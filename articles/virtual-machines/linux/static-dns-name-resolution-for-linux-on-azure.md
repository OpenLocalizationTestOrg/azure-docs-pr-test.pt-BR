---
title: "aaaUse resolução com hello 2.0 do CLI do Azure de nome de DNS interno de VM | Microsoft Docs"
description: "Como a rede virtual toocreate placas de interface e usar interno do DNS para resolução de nome VM no Azure com hello 2.0 do CLI do Azure"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="292a7-103">Criar placas de adaptador de rede virtual e usar DNS interno para resolução de nome da VM no Azure</span><span class="sxs-lookup"><span data-stu-id="292a7-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span></span>
<span data-ttu-id="292a7-104">Este artigo mostra como tooset estático internos nomes DNS para VMs do Linux usando virtual rede placas de interface (vNics) e nomes de rótulo DNS com hello 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="292a7-104">This article shows you how tooset static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with hello Azure CLI 2.0.</span></span> <span data-ttu-id="292a7-105">Você também pode executar essas etapas com hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="292a7-105">You can also perform these steps with hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="292a7-106">Nomes DNS estáticos são usados para serviços de infraestrutura permanentes como um servidor de build Jenkins, que é usado para este documento ou um servidor Git.</span><span class="sxs-lookup"><span data-stu-id="292a7-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="292a7-107">requisitos de saudação são:</span><span class="sxs-lookup"><span data-stu-id="292a7-107">hello requirements are:</span></span>

* [<span data-ttu-id="292a7-108">uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="292a7-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="292a7-109">arquivos de chave SSH pública e privada</span><span class="sxs-lookup"><span data-stu-id="292a7-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="292a7-110">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="292a7-110">Quick commands</span></span>
<span data-ttu-id="292a7-111">Se você precisar tooquickly realizar tarefa hello, Olá seção a seguir fornece detalhes sobre comandos Olá necessários.</span><span class="sxs-lookup"><span data-stu-id="292a7-111">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="292a7-112">Obter mais informações e o contexto para cada etapa pode ser encontrada no restante de saudação do documento hello, [Iniciar aqui](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="292a7-112">More detailed information and context for each step can be found in hello rest of hello document, [starting here](#detailed-walkthrough).</span></span> <span data-ttu-id="292a7-113">tooperform essas etapas, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="292a7-113">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="292a7-114">Pré-requisitos: grupo de recursos, rede virtual e sub-rede, grupo de segurança de rede com o SSH de entrada.</span><span class="sxs-lookup"><span data-stu-id="292a7-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span></span>

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a><span data-ttu-id="292a7-115">Criar uma placa de interface de rede virtual com um nome DNS interno estático</span><span class="sxs-lookup"><span data-stu-id="292a7-115">Create a virtual network interface card with a static internal DNS name</span></span>
<span data-ttu-id="292a7-116">Criar hello vNic com [nic da rede az criar](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="292a7-116">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="292a7-117">Olá `--internal-dns-name` sinalizador CLI é para o rótulo DNS Olá de configuração, que fornece o nome DNS estático de saudação de placa de interface de rede virtual (vNic) de saudação.</span><span class="sxs-lookup"><span data-stu-id="292a7-117">hello `--internal-dns-name` CLI flag is for setting hello DNS label, which provides hello static DNS name for hello virtual network interface card (vNic).</span></span> <span data-ttu-id="292a7-118">Olá, exemplo a seguir cria uma vNic denominada `myNic`, conecta toohello `myVnet` rede virtual e cria um registro de nome DNS interno chamado `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="292a7-118">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a><span data-ttu-id="292a7-119">Implantar uma VM e conecte-se Olá vNic</span><span class="sxs-lookup"><span data-stu-id="292a7-119">Deploy a VM and connect hello vNic</span></span>
<span data-ttu-id="292a7-120">Crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="292a7-120">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="292a7-121">Olá `--nics` sinalizador conecta Olá vNic toohello VM durante a saudação tooAzure de implantação.</span><span class="sxs-lookup"><span data-stu-id="292a7-121">hello `--nics` flag connects hello vNic toohello VM during hello deployment tooAzure.</span></span> <span data-ttu-id="292a7-122">Olá, exemplo a seguir cria uma VM denominada `myVM` com discos gerenciado do Azure e anexa Olá vNic denominado `myNic` de saudação anterior etapa:</span><span class="sxs-lookup"><span data-stu-id="292a7-122">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="292a7-123">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="292a7-123">Detailed walkthrough</span></span>

<span data-ttu-id="292a7-124">Uma implantação contínua (CiCd) e integração contínua completo infra-estrutura no Azure exige que determinados servidores de servidores toobe vida longa ou estático.</span><span class="sxs-lookup"><span data-stu-id="292a7-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span> <span data-ttu-id="292a7-125">É recomendável que os ativos do Azure como Olá redes virtuais e grupos de segurança de rede são estáticos e vida útil longa recursos que raramente são implantados.</span><span class="sxs-lookup"><span data-stu-id="292a7-125">It is recommended that Azure assets like hello virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="292a7-126">Quando uma rede virtual tiver sido implantada, ele pode ser reutilizado por novas implantações sem nenhuma infraestrutura de toohello efeitos adversos.</span><span class="sxs-lookup"><span data-stu-id="292a7-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="292a7-127">Mais tarde, você pode adicionar um servidor de repositório Git ou um servidor de automação Jenkins oferece a rede virtual do CiCd toothis para seus ambientes de desenvolvimento ou teste.</span><span class="sxs-lookup"><span data-stu-id="292a7-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd toothis virtual network for your development or test environments.</span></span>  

<span data-ttu-id="292a7-128">Nomes DNS internos podem ser resolvidos apenas em uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="292a7-128">Internal DNS names are only resolvable inside an Azure virtual network.</span></span> <span data-ttu-id="292a7-129">Como os nomes DNS Olá são internos, eles não são toohello resolvível fora da internet, fornecendo a infra-estrutura de toohello de segurança adicional.</span><span class="sxs-lookup"><span data-stu-id="292a7-129">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="292a7-130">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="292a7-130">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="292a7-131">Os nomes de parâmetro de exemplo incluem `myResourceGroup`, `myNic` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="292a7-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="292a7-132">Criar grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="292a7-132">Create hello resource group</span></span>
<span data-ttu-id="292a7-133">Primeiro, crie o grupo de recursos de saudação com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="292a7-133">First, create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="292a7-134">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westus` local:</span><span class="sxs-lookup"><span data-stu-id="292a7-134">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="292a7-135">Criar rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="292a7-135">Create hello virtual network</span></span>

<span data-ttu-id="292a7-136">Olá próxima etapa é toobuild toolaunch uma rede virtual Olá VMs em.</span><span class="sxs-lookup"><span data-stu-id="292a7-136">hello next step is toobuild a virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="292a7-137">rede virtual Olá contém uma sub-rede para este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="292a7-137">hello virtual network contains one subnet for this walkthrough.</span></span> <span data-ttu-id="292a7-138">Para obter mais informações sobre redes virtuais do Azure, consulte [criar uma rede virtual usando Olá CLI do Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="292a7-138">For more information on Azure virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="292a7-139">Criar rede virtual de saudação com [criar redes de rede az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="292a7-139">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="292a7-140">Olá, exemplo a seguir cria uma rede virtual denominada `myVnet` e sub-rede denominada `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="292a7-140">hello following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="292a7-141">Criar grupo de segurança de rede de saudação</span><span class="sxs-lookup"><span data-stu-id="292a7-141">Create hello Network Security Group</span></span>
<span data-ttu-id="292a7-142">Grupos de segurança de rede do Azure são equivalentes tooa firewall na camada de rede hello.</span><span class="sxs-lookup"><span data-stu-id="292a7-142">Azure Network Security Groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="292a7-143">Para obter mais informações sobre grupos de segurança de rede, consulte [como NSGs toocreate em Olá CLI do Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="292a7-143">For more information about Network Security Groups, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="292a7-144">Criar grupo de segurança de rede Olá com [criar az rede nsg](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="292a7-144">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="292a7-145">Olá, exemplo a seguir cria um grupo de segurança de rede denominado `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="292a7-145">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a><span data-ttu-id="292a7-146">Adicionar uma regra de entrada de tooallow SSH</span><span class="sxs-lookup"><span data-stu-id="292a7-146">Add an inbound rule tooallow SSH</span></span>
<span data-ttu-id="292a7-147">Adicionar uma regra de entrada para o grupo de segurança de rede Olá com [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="292a7-147">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="292a7-148">Olá, exemplo a seguir cria uma regra denominada `myRuleAllowSSH`:</span><span class="sxs-lookup"><span data-stu-id="292a7-148">hello following example creates a rule named `myRuleAllowSSH`:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a><span data-ttu-id="292a7-149">Associar sub-redes Olá Olá grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="292a7-149">Associate hello subnet with hello Network Security Group</span></span>
<span data-ttu-id="292a7-150">tooassociate sub-rede Olá Olá grupo de segurança de rede, use [atualização de sub-rede da rede virtual de rede az](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="292a7-150">tooassociate hello subnet with hello Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span></span> <span data-ttu-id="292a7-151">Hello, exemplo a seguir associa o nome de sub-rede Olá `mySubnet` com hello grupo de segurança de rede denominado `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="292a7-151">hello following example associates hello subnet name `mySubnet` with hello Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a><span data-ttu-id="292a7-152">Criar a placa de interface de rede virtual hello e nomes DNS estático</span><span class="sxs-lookup"><span data-stu-id="292a7-152">Create hello virtual network interface card and static DNS names</span></span>
<span data-ttu-id="292a7-153">O Azure é muito flexível, mas toouse nomes DNS para resolução de nome VM, você precisa de placas de interface de rede virtual toocreate (vNics) que incluem um rótulo DNS.</span><span class="sxs-lookup"><span data-stu-id="292a7-153">Azure is very flexible, but toouse DNS names for VM name resolution, you need toocreate virtual network interface cards (vNics) that include a DNS label.</span></span> <span data-ttu-id="292a7-154">vNics são importantes para você pode reutilizá-los, conectando-os VMs toodifferent ciclo de vida de infraestrutura de saudação.</span><span class="sxs-lookup"><span data-stu-id="292a7-154">vNics are important as you can reuse them by connecting them toodifferent VMs over hello infrastructure lifecycle.</span></span> <span data-ttu-id="292a7-155">Essa abordagem mantém Olá vNic como um recurso estático enquanto Olá VMs pode ser temporário.</span><span class="sxs-lookup"><span data-stu-id="292a7-155">This approach keeps hello vNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="292a7-156">Usando o DNS rotulagem no vNic hello, estamos tooenable capaz de resolução de nome simples de outras VMs em redes de saudação.</span><span class="sxs-lookup"><span data-stu-id="292a7-156">By using DNS labeling on hello vNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span> <span data-ttu-id="292a7-157">Usando nomes resolvível permite que outro servidor de automação VMs tooaccess Olá por nome DNS Olá `Jenkins` ou servidor de Git hello como `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="292a7-157">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  

<span data-ttu-id="292a7-158">Criar hello vNic com [nic da rede az criar](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="292a7-158">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="292a7-159">Olá, exemplo a seguir cria uma vNic denominada `myNic`, conecta toohello `myVnet` rede virtual denominado `myVnet`e cria um registro de nome DNS interno chamado `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="292a7-159">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="292a7-160">Implantar Olá VM na infraestrutura de rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="292a7-160">Deploy hello VM into hello virtual network infrastructure</span></span>
<span data-ttu-id="292a7-161">Agora temos uma rede virtual e sub-rede, um grupo de segurança de rede atuando como um firewall tooprotect nosso sub-rede bloqueando todo o tráfego de entrada exceto porta 22 para SSH e uma vNic.</span><span class="sxs-lookup"><span data-stu-id="292a7-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span></span> <span data-ttu-id="292a7-162">Agora a VM pode ser implantada nessa infraestrutura de rede existente.</span><span class="sxs-lookup"><span data-stu-id="292a7-162">You can now deploy a VM inside this existing network infrastructure.</span></span>

<span data-ttu-id="292a7-163">Crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="292a7-163">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="292a7-164">Olá, exemplo a seguir cria uma VM denominada `myVM` com discos gerenciado do Azure e anexa Olá vNic denominado `myNic` de saudação anterior etapa:</span><span class="sxs-lookup"><span data-stu-id="292a7-164">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="292a7-165">Usando Olá CLI sinalizadores de toocall recursos existentes, podemos instruir Olá toodeploy Azure VM dentro da rede existente hello.</span><span class="sxs-lookup"><span data-stu-id="292a7-165">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="292a7-166">tooreiterate, depois que uma rede virtual e a sub-rede forem implantados, eles podem ser mantidos como estáticos ou permanentes de recursos dentro de sua região do Azure.</span><span class="sxs-lookup"><span data-stu-id="292a7-166">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="292a7-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="292a7-167">Next steps</span></span>
* [<span data-ttu-id="292a7-168">Criar seu próprio ambiente personalizado para uma VM do Linux usando os comandos da CLI do Azure diretamente</span><span class="sxs-lookup"><span data-stu-id="292a7-168">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="292a7-169">Criar uma VM do Linux no Azure usando modelos</span><span class="sxs-lookup"><span data-stu-id="292a7-169">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
