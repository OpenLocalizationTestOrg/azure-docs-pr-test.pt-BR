---
title: aaaDeploy VMs do Linux em uma rede existente com o Azure CLI 2.0 | Microsoft Docs
description: "Saiba como toodeploy uma máquina virtual do Linux em uma rede Virtual existente usando Olá 2.0 do CLI do Azure"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a><span data-ttu-id="bfe82-103">Como toodeploy uma máquina virtual do Linux em uma rede Virtual do Azure existente com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="bfe82-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI</span></span>

<span data-ttu-id="bfe82-104">Este artigo mostra como toouse hello Azure CLI 2.0 toodeploy uma máquina virtual (VM) em uma rede virtual existente.</span><span class="sxs-lookup"><span data-stu-id="bfe82-104">This article shows you how toouse hello Azure CLI 2.0 toodeploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="bfe82-105">requisitos de saudação são:</span><span class="sxs-lookup"><span data-stu-id="bfe82-105">hello requirements are:</span></span>

- [<span data-ttu-id="bfe82-106">uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="bfe82-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="bfe82-107">arquivos de chave SSH pública e privada</span><span class="sxs-lookup"><span data-stu-id="bfe82-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

<span data-ttu-id="bfe82-108">Você também pode executar essas etapas com hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="bfe82-108">You can also perform these steps with hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="bfe82-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="bfe82-109">Quick Commands</span></span>
<span data-ttu-id="bfe82-110">Se você precisar tooquickly realizar tarefa hello, Olá seção a seguir fornece detalhes sobre comandos Olá necessários.</span><span class="sxs-lookup"><span data-stu-id="bfe82-110">If you need tooquickly accomplish hello task, hello following section details hello  commands needed.</span></span> <span data-ttu-id="bfe82-111">Obter mais informações e o contexto para cada etapa pode ser encontrada restante de saudação do documento hello, [Iniciar aqui](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="bfe82-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="bfe82-112">toocreate nesse ambiente personalizado, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado no tooan conta do Azure usando [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="bfe82-112">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="bfe82-113">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="bfe82-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="bfe82-114">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="bfe82-114">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

<span data-ttu-id="bfe82-115">**Pré-requisitos:** grupo de recursos do Azure, rede virtual e sub-rede, grupo de segurança de rede com o SSH de entrada e uma placa de interface de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="bfe82-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="bfe82-116">Implantar Olá VM na infraestrutura de rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="bfe82-116">Deploy hello VM into hello virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="bfe82-117">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="bfe82-117">Detailed walkthrough</span></span>

<span data-ttu-id="bfe82-118">Os ativos do Azure, como as redes virtuais e os grupos de segurança de rede, devem ser recursos estáticos e de longa duração que raramente são implantados.</span><span class="sxs-lookup"><span data-stu-id="bfe82-118">Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="bfe82-119">Quando uma rede virtual tiver sido implantada, ele pode ser reutilizado por novas implantações sem nenhuma infraestrutura de toohello efeitos adversos.</span><span class="sxs-lookup"><span data-stu-id="bfe82-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="bfe82-120">Pensar em uma rede virtual como sendo um comutador de rede de hardware tradicional - você não precisará tooconfigure alternar de um novo hardware com cada implantação.</span><span class="sxs-lookup"><span data-stu-id="bfe82-120">Think about a virtual network as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="bfe82-121">Com uma rede virtual configurada corretamente, você pode continuar toodeploy novas VMs na rede virtual repetidamente com poucas, se houver, as alterações necessárias durante o tempo de saudação da rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="bfe82-121">With a correctly configured virtual network, you can continue toodeploy new VMs into that virtual network over and over with few, if any, changes required over hello life of hello virtual network.</span></span>

<span data-ttu-id="bfe82-122">toocreate nesse ambiente personalizado, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado no tooan conta do Azure usando [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="bfe82-122">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="bfe82-123">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="bfe82-123">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="bfe82-124">Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myVnet* e *myVM*.</span><span class="sxs-lookup"><span data-stu-id="bfe82-124">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="bfe82-125">Criar grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="bfe82-125">Create hello resource group</span></span>

<span data-ttu-id="bfe82-126">Primeiro, crie um tooorganize do grupo de recursos do Azure tudo que você cria neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="bfe82-126">First, create an Azure resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="bfe82-127">Para saber mais sobre grupos de recursos, confira [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bfe82-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="bfe82-128">Criar grupo de recursos de saudação com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="bfe82-128">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="bfe82-129">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="bfe82-129">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="bfe82-130">Criar rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="bfe82-130">Create hello virtual network</span></span>

<span data-ttu-id="bfe82-131">Permite criar uma saudação toolaunch de rede virtual do Azure VMs em.</span><span class="sxs-lookup"><span data-stu-id="bfe82-131">Lets build an Azure virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="bfe82-132">Para obter mais informações sobre redes virtuais, consulte [criar uma rede virtual usando Olá CLI do Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bfe82-132">For more information on virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span></span> <span data-ttu-id="bfe82-133">Criar rede virtual de saudação com [criar redes de rede az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="bfe82-133">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="bfe82-134">Olá, exemplo a seguir cria uma rede virtual denominada *myVnet* e sub-rede denominada *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="bfe82-134">hello following example creates a virtual network named *myVnet* and subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="bfe82-135">Criar grupo de segurança de rede Olá</span><span class="sxs-lookup"><span data-stu-id="bfe82-135">Create hello network security group</span></span>

<span data-ttu-id="bfe82-136">Grupos de segurança de rede do Azure são equivalentes tooa firewall na camada de rede hello.</span><span class="sxs-lookup"><span data-stu-id="bfe82-136">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="bfe82-137">Para obter mais informações sobre os grupos de segurança de rede, consulte [como os grupos de segurança de rede toocreate em Olá CLI do Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bfe82-137">For more information on network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span> <span data-ttu-id="bfe82-138">Criar grupo de segurança de rede Olá com [criar az rede nsg](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="bfe82-138">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="bfe82-139">Olá, exemplo a seguir cria um grupo de segurança de rede denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="bfe82-139">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="bfe82-140">Adicionar uma regra de permissão de SSH de entrada</span><span class="sxs-lookup"><span data-stu-id="bfe82-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="bfe82-141">Olá VM precisa ter acesso de saudação à internet, para que uma regra que permite a porta de entrada 22 tráfego toobe passado Olá rede tooport 22 na Olá VM é necessária.</span><span class="sxs-lookup"><span data-stu-id="bfe82-141">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span> <span data-ttu-id="bfe82-142">Adicionar uma regra de entrada para o grupo de segurança de rede Olá com [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="bfe82-142">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="bfe82-143">Olá, exemplo a seguir cria uma regra denominada *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="bfe82-143">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a><span data-ttu-id="bfe82-144">Anexar o grupo de segurança de rede do hello sub-rede toohello</span><span class="sxs-lookup"><span data-stu-id="bfe82-144">Attach hello subnet toohello network security group</span></span>

<span data-ttu-id="bfe82-145">regras de grupo de segurança de rede Olá podem ser aplicado tooa sub-rede ou uma interface de rede virtual específica.</span><span class="sxs-lookup"><span data-stu-id="bfe82-145">hello network security group rules can be applied tooa subnet or a specific virtual network interface.</span></span> <span data-ttu-id="bfe82-146">Permite anexar Olá segurança grupo tooour sub-rede.</span><span class="sxs-lookup"><span data-stu-id="bfe82-146">Lets attach hello network security group tooour subnet.</span></span> <span data-ttu-id="bfe82-147">Conecte seu grupo de segurança de rede toohello sub-rede com [atualização de sub-rede da rede virtual de rede az](/cli/azure/network/vnet/subnet#update):</span><span class="sxs-lookup"><span data-stu-id="bfe82-147">Attach your subnet toohello network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a><span data-ttu-id="bfe82-148">Adicionar uma sub-rede toohello de placa de interface de rede virtual</span><span class="sxs-lookup"><span data-stu-id="bfe82-148">Add a virtual network interface card toohello subnet</span></span>

<span data-ttu-id="bfe82-149">Placas de interface de rede virtual (VNics) são importantes para você pode reutilizá-los, conectando-os toodifferent VMs.</span><span class="sxs-lookup"><span data-stu-id="bfe82-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="bfe82-150">Essa reutilização permite tookeep Olá VNic como um recurso estático enquanto Olá VMs pode ser temporário.</span><span class="sxs-lookup"><span data-stu-id="bfe82-150">This reuse allows you tookeep hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="bfe82-151">Criar uma VNic e associá-lo a sub-rede Olá [nic da rede az criar](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="bfe82-151">Create a VNic and associate it with hello subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="bfe82-152">Olá, exemplo a seguir cria uma VNic denominada *myNic*:</span><span class="sxs-lookup"><span data-stu-id="bfe82-152">hello following example creates a VNic named *myNic*:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="bfe82-153">Implantar Olá VM na infraestrutura de rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="bfe82-153">Deploy hello VM into hello virtual network infrastructure</span></span>

<span data-ttu-id="bfe82-154">Agora, você tem uma rede virtual e sub-redes e uma sub-rede da rede segurança grupo tooprotect Olá bloqueando todo o tráfego de entrada exceto 22 de porta para o SSH.</span><span class="sxs-lookup"><span data-stu-id="bfe82-154">You now have a virtual network and subnet, and a network security group tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="bfe82-155">Olá VM agora pode ser implantado nessa infraestrutura de rede existente.</span><span class="sxs-lookup"><span data-stu-id="bfe82-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="bfe82-156">Crie a sua VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="bfe82-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="bfe82-157">Para obter mais informações sobre Olá sinalizadores toouse com hello Azure CLI 2.0 toodeploy uma VM completa, consulte [criar um ambiente completo do Linux usando Olá CLI do Azure](create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="bfe82-157">For more information on hello flags toouse with hello Azure CLI 2.0 toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md).</span></span>

<span data-ttu-id="bfe82-158">saudação de exemplo a seguir cria uma máquina virtual usando discos gerenciado do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfe82-158">hello following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="bfe82-159">Esses discos são manipulados pelo Olá plataforma Windows Azure e não exigem qualquer etapa de preparação ou local toostore-los.</span><span class="sxs-lookup"><span data-stu-id="bfe82-159">These disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="bfe82-160">Para saber mais sobre discos gerenciados, veja [Visão geral dos Azure Managed Disks](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bfe82-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="bfe82-161">Se desejar que os discos toouse não gerenciado, consulte a Observação adicionais de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="bfe82-161">If you wish toouse unmanaged disks, see hello additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

<span data-ttu-id="bfe82-162">Se você usar discos gerenciados, ignore esta etapa.</span><span class="sxs-lookup"><span data-stu-id="bfe82-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="bfe82-163">Se desejar que os discos toouse não gerenciado, você precisa tooadd Olá seguintes parâmetros adicionais toohello continuar comando toocreate não gerenciado discos na conta de armazenamento Olá chamado `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="bfe82-163">If you wish toouse unmanaged disks, you need tooadd hello following additional parameters toohello proceeding command toocreate unmanaged disks in hello storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="bfe82-164">Usando Olá CLI sinalizadores de toocall recursos existentes, você instruir Olá toodeploy Azure VM dentro da rede existente hello.</span><span class="sxs-lookup"><span data-stu-id="bfe82-164">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="bfe82-165">Depois que uma rede virtual e uma sub-rede são implantadas, elas podem ser mantidas como recursos estáticos ou permanentes na sua região do Azure.</span><span class="sxs-lookup"><span data-stu-id="bfe82-165">Once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="bfe82-166">Neste exemplo, você não criar e atribuir um toohello de endereço IP público VNic, portanto essa VM não é publicamente acessível pela Internet da saudação.</span><span class="sxs-lookup"><span data-stu-id="bfe82-166">In this example, you did not create and assign a public IP address toohello VNic, so this VM is not publicly accessible over hello Internet.</span></span> <span data-ttu-id="bfe82-167">Para obter mais informações, consulte [criar uma VM com um IP público estático usando Olá CLI do Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="bfe82-167">For more information, see [Create a VM with a static public IP using hello Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfe82-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bfe82-168">Next steps</span></span>
<span data-ttu-id="bfe82-169">Para obter mais informações sobre maneiras toocreate as máquinas virtuais no Azure, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bfe82-169">For more information about ways toocreate virtual machines in Azure, see hello following resources:</span></span>

* [<span data-ttu-id="bfe82-170">Usar um modelo de Gerenciador de recursos do Azure toocreate uma implantação específica</span><span class="sxs-lookup"><span data-stu-id="bfe82-170">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="bfe82-171">Criar seu próprio ambiente personalizado para uma VM do Linux usando os comandos da CLI do Azure diretamente</span><span class="sxs-lookup"><span data-stu-id="bfe82-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="bfe82-172">Criar uma VM do Linux no Azure usando modelos</span><span class="sxs-lookup"><span data-stu-id="bfe82-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
