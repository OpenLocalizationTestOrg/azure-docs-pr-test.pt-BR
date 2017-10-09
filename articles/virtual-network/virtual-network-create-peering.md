---
title: aaaCreate um emparelhamento de rede virtual do Azure - Gerenciador de recursos - mesma assinatura | Microsoft Docs
description: Saiba como toocreate um emparelhamento de rede virtual entre redes virtuais criadas por meio de Gerenciador de recursos que existem no hello mesmo assinatura do Azure.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a><span data-ttu-id="67af8-103">Criar um emparelhamento de rede virtual – Resource Manager, mesma assinatura</span><span class="sxs-lookup"><span data-stu-id="67af8-103">Create a virtual network peering - Resource Manager, same subscription</span></span>

<span data-ttu-id="67af8-104">Neste tutorial, você aprenderá toocreate uma emparelhamento entre redes virtuais criadas por meio do Gerenciador de recursos de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="67af8-104">In this tutorial, you learn toocreate a virtual network peering between virtual networks created through Resource Manager.</span></span> <span data-ttu-id="67af8-105">Ambas as redes virtuais existirem no hello mesmo assinatura.</span><span class="sxs-lookup"><span data-stu-id="67af8-105">Both virtual networks exist in hello same subscription.</span></span> <span data-ttu-id="67af8-106">Emparelhamento duas redes virtuais habilita recursos toocommunicate redes virtuais diferentes entre si com hello mesma largura de banda e latência, como se foram recursos Olá no hello mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="67af8-106">Peering two virtual networks enables resources in different virtual networks toocommunicate with each other with hello same bandwidth and latency as though hello resources were in hello same virtual network.</span></span> <span data-ttu-id="67af8-107">Saiba mais sobre [Emparelhamento de rede virtual](virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67af8-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="67af8-108">Olá etapas toocreate um emparelhamento de rede virtual são diferentes, dependendo se as redes virtuais Olá estão em Olá igual ou diferente, assinaturas e qual [modelo de implantação do Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Olá as redes virtuais são criadas a.</span><span class="sxs-lookup"><span data-stu-id="67af8-108">hello steps toocreate a virtual network peering are different, depending on whether hello virtual networks are in hello same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello virtual networks are created through.</span></span> <span data-ttu-id="67af8-109">Saiba como toocreate um virtual rede emparelhamento em outros cenários, clicando em cenário de saudação do hello a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="67af8-109">Learn how toocreate a virtual network peering in other scenarios by clicking hello scenario from hello following table:</span></span>

|<span data-ttu-id="67af8-110">Modelo de implantação do Azure</span><span class="sxs-lookup"><span data-stu-id="67af8-110">Azure deployment model</span></span>  | <span data-ttu-id="67af8-111">Assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="67af8-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="67af8-112">Ambos Resource Manager</span><span class="sxs-lookup"><span data-stu-id="67af8-112">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="67af8-113">Diferente</span><span class="sxs-lookup"><span data-stu-id="67af8-113">Different</span></span>|
|[<span data-ttu-id="67af8-114">Um Resource Manager, um clássico</span><span class="sxs-lookup"><span data-stu-id="67af8-114">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="67af8-115">Idêntico</span><span class="sxs-lookup"><span data-stu-id="67af8-115">Same</span></span>|
|[<span data-ttu-id="67af8-116">Um Resource Manager, um clássico</span><span class="sxs-lookup"><span data-stu-id="67af8-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="67af8-117">Diferente</span><span class="sxs-lookup"><span data-stu-id="67af8-117">Different</span></span>|

<span data-ttu-id="67af8-118">Não é possível criar um emparelhamento de rede virtual entre duas redes virtuais implantadas por meio do modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="67af8-118">A virtual network peering cannot be created between two virtual networks deployed through hello classic deployment model.</span></span> <span data-ttu-id="67af8-119">Um emparelhamento de rede virtual só pode ser criado entre duas redes virtuais que existem no hello mesma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="67af8-119">A virtual network peering can only be created between two virtual networks that exist in hello same Azure region.</span></span> <span data-ttu-id="67af8-120">Se você precisar tooconnect as redes virtuais que foram criados por meio do modelo de implantação clássico hello, ou que existe em diferentes regiões do Azure, você pode usar um Azure [Gateway VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Olá redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="67af8-120">If you need tooconnect virtual networks that were both created through hello classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello virtual networks.</span></span> 

<span data-ttu-id="67af8-121">Você pode usar o hello [portal do Azure](#portal), hello Azure [interface de linha de comando](#cli) (CLI), Azure [PowerShell](#powershell), ou um [modelo do Azure Resource Manager](#template) toocreate um emparelhamento de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="67af8-121">You can use hello [Azure portal](#portal), hello Azure [command-line interface](#cli) (CLI), Azure [PowerShell](#powershell), or an [Azure Resource Manager template](#template) toocreate a virtual network peering.</span></span> <span data-ttu-id="67af8-122">Clique em qualquer Olá anterior ferramenta links toogo diretamente toohello as etapas para criar uma rede virtual emparelhamento usando sua ferramenta de escolha.</span><span class="sxs-lookup"><span data-stu-id="67af8-122">Click any of hello previous tool links toogo directly toohello steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="67af8-123"><a name="portal"></a>Criar emparelhamento – portal do Azure</span><span class="sxs-lookup"><span data-stu-id="67af8-123"><a name="portal"></a>Create peering - Azure portal</span></span>

1. <span data-ttu-id="67af8-124">Faça logon no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67af8-124">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="67af8-125">conta Olá com que log deve ter Olá permissões necessárias toocreate um emparelhamento de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="67af8-125">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="67af8-126">Consulte Olá [permissões](#permissions) deste artigo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="67af8-126">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="67af8-127">Clique em **+ Novo**, em **Rede** e, em seguida, em **Rede virtual**.</span><span class="sxs-lookup"><span data-stu-id="67af8-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="67af8-128">Em Olá **criar rede virtual** folha, inserir, ou selecione os valores para Olá configurações a seguir e clique em **criar**:</span><span class="sxs-lookup"><span data-stu-id="67af8-128">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="67af8-129">**Nome**: *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="67af8-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="67af8-130">**Espaço de endereço**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="67af8-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="67af8-131">**Nome da sub-rede**: *padrão*</span><span class="sxs-lookup"><span data-stu-id="67af8-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="67af8-132">**Intervalo de endereços da sub-rede**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="67af8-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="67af8-133">**Assinatura**: selecione sua assinatura</span><span class="sxs-lookup"><span data-stu-id="67af8-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="67af8-134">**Grupo de recursos**: selecione **Criar novo** e insira *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="67af8-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="67af8-135">**Localização**: *Leste dos EUA*</span><span class="sxs-lookup"><span data-stu-id="67af8-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="67af8-136">Conclua as etapas 2-3 novamente especificando Olá valores na etapa 3 a seguir:</span><span class="sxs-lookup"><span data-stu-id="67af8-136">Complete steps 2-3 again specifying hello following values in step 3:</span></span>
    - <span data-ttu-id="67af8-137">**Nome**: *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="67af8-137">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="67af8-138">**Espaço de endereço**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="67af8-138">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="67af8-139">**Nome da sub-rede**: *padrão*</span><span class="sxs-lookup"><span data-stu-id="67af8-139">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="67af8-140">**Intervalo de endereços da sub-rede**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="67af8-140">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="67af8-141">**Assinatura**: selecione sua assinatura</span><span class="sxs-lookup"><span data-stu-id="67af8-141">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="67af8-142">**Grupo de recursos**: selecione **Usar existente** e selecione *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="67af8-142">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="67af8-143">**Localização**: *Leste dos EUA*</span><span class="sxs-lookup"><span data-stu-id="67af8-143">**Location**: *East US*</span></span>
5. <span data-ttu-id="67af8-144">Em Olá **pesquisar recursos** caixa na parte superior de saudação do portal hello, tipo *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="67af8-144">In hello **Search resources** box at hello top of hello portal, type *myResourceGroup*.</span></span> <span data-ttu-id="67af8-145">Clique em **myResourceGroup** quando ele aparece nos resultados da pesquisa hello.</span><span class="sxs-lookup"><span data-stu-id="67af8-145">Click **myResourceGroup** when it appears in hello search results.</span></span> <span data-ttu-id="67af8-146">Uma folha é exibido para Olá **myresourcegroup** grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="67af8-146">A blade appears for hello **myresourcegroup** resource group.</span></span> <span data-ttu-id="67af8-147">grupo de recursos de saudação contém Olá duas redes virtuais criadas nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="67af8-147">hello resource group contains hello two virtual networks created in previous steps.</span></span>
6. <span data-ttu-id="67af8-148">Clique em **myVNet1**.</span><span class="sxs-lookup"><span data-stu-id="67af8-148">Click **myVNet1**.</span></span>
7. <span data-ttu-id="67af8-149">Em Olá **myVnet1** folha que aparece, clique em **emparelhamentos** da lista de vertical Olá opções Olá lado esquerdo da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="67af8-149">In hello **myVnet1** blade that appears, click **Peerings** from hello vertical list of options on hello left side of hello blade.</span></span>
8. <span data-ttu-id="67af8-150">Em Olá **myVnet1 - emparelhamentos** folha que aparecer, clique em **+ adicionar**</span><span class="sxs-lookup"><span data-stu-id="67af8-150">In hello **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
9. <span data-ttu-id="67af8-151">Em Olá **adicionar emparelhamento** folha que aparece, digite, ou selecione Olá as opções a seguir e clique em **Okey**:</span><span class="sxs-lookup"><span data-stu-id="67af8-151">In hello **Add peering** blade that appears, enter, or select hello following options, then click **OK**:</span></span>
     - <span data-ttu-id="67af8-152">**Nome**: *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="67af8-152">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="67af8-153">**Modelo de implantação de rede virtual**: selecione **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="67af8-153">**Virtual network deployment model**:  Select **Resource Manager**.</span></span> 
     - <span data-ttu-id="67af8-154">**Assinatura**: selecione sua assinatura</span><span class="sxs-lookup"><span data-stu-id="67af8-154">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="67af8-155">**Rede virtual**: clique em **Escolher uma rede virtual** e, em seguida, clique em **myVnet2**.</span><span class="sxs-lookup"><span data-stu-id="67af8-155">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="67af8-156">**Permitir acesso à rede virtual:** verifique se a opção **Habilitado** está selecionada.</span><span class="sxs-lookup"><span data-stu-id="67af8-156">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="67af8-157">Nenhuma outra configuração é usada neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="67af8-157">No other settings are used in this tutorial.</span></span> <span data-ttu-id="67af8-158">ler toolearn sobre todas as configurações de emparelhamento, [gerenciar emparelhamentos de rede virtual](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="67af8-158">toolearn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
10. <span data-ttu-id="67af8-159">Depois de clicar em **Okey** na etapa anterior de saudação, Olá **adicionar emparelhamento** folha fecha e consulte Olá **myVnet1 - emparelhamentos** folha novamente.</span><span class="sxs-lookup"><span data-stu-id="67af8-159">After clicking **OK** in hello previous step, hello **Add peering** blade closes and you see hello **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="67af8-160">Depois de alguns segundos, Olá emparelhamento que você criou aparece na folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="67af8-160">After a few seconds, hello peering you created appears in hello blade.</span></span> <span data-ttu-id="67af8-161">**Iniciada** está listado no hello **STATUS EMPARELHAMENTO** coluna Olá **myVnet1ToMyVnet2** emparelhamento é criado.</span><span class="sxs-lookup"><span data-stu-id="67af8-161">**Initiated** is listed in hello **PEERING STATUS** column for hello **myVnet1ToMyVnet2** peering you created.</span></span> <span data-ttu-id="67af8-162">Você emparelhadas tooVnet2 Vnet1, mas agora myVnet2 toomyVnet1 deve ser par.</span><span class="sxs-lookup"><span data-stu-id="67af8-162">You've peered Vnet1 tooVnet2, but now you must peer myVnet2 toomyVnet1.</span></span> <span data-ttu-id="67af8-163">Olá emparelhamento deve ser criado em ambas as direções tooenable recursos Olá toocommunicate de redes virtuais entre si.</span><span class="sxs-lookup"><span data-stu-id="67af8-163">hello peering must be created in both directions tooenable resources in hello virtual networks toocommunicate with each other.</span></span>
11. <span data-ttu-id="67af8-164">Conclua as etapas 5 a 10 novamente para a myVnet2.</span><span class="sxs-lookup"><span data-stu-id="67af8-164">Complete steps 5-10 again for myVnet2.</span></span>  <span data-ttu-id="67af8-165">Nome hello emparelhamento *myVnet2ToMyVnet1*.</span><span class="sxs-lookup"><span data-stu-id="67af8-165">Name hello peering *myVnet2ToMyVnet1*.</span></span>
12. <span data-ttu-id="67af8-166">Alguns segundos depois de clicar em **Okey** toocreate Olá emparelhamento para MyVnet2, hello **myVnet2ToMyVnet1** emparelhamento você acabou de criar está listado com **conectado** em Olá  **STATUS de EMPARELHAMENTO** coluna.</span><span class="sxs-lookup"><span data-stu-id="67af8-166">A few seconds after clicking **OK** toocreate hello peering for MyVnet2, hello **myVnet2ToMyVnet1** peering you just created is listed with **Connected** in hello **PEERING STATUS** column.</span></span>
13. <span data-ttu-id="67af8-167">Conclua as etapas 5 a 7 novamente para a MyVnet1.</span><span class="sxs-lookup"><span data-stu-id="67af8-167">Complete steps 5-7 again for MyVnet1.</span></span> <span data-ttu-id="67af8-168">Olá **STATUS EMPARELHAMENTO** para Olá **myVnet1ToVNet2** emparelhamento agora também está **conectado**.</span><span class="sxs-lookup"><span data-stu-id="67af8-168">hello **PEERING STATUS** for hello **myVnet1ToVNet2** peering is now also **Connected**.</span></span> <span data-ttu-id="67af8-169">Olá emparelhamento é estabelecida com êxito depois de ver **conectado** em Olá **STATUS EMPARELHAMENTO** coluna para ambas as redes virtuais no emparelhamento via protocolo hello.</span><span class="sxs-lookup"><span data-stu-id="67af8-169">hello peering is successfully established after you see **Connected** in hello **PEERING STATUS** column for both virtual networks in hello peering.</span></span>
14. <span data-ttu-id="67af8-170">**Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.</span><span class="sxs-lookup"><span data-stu-id="67af8-170">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
15. <span data-ttu-id="67af8-171">**Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em Olá [excluir recursos](#delete-portal) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="67af8-171">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete-portal) section of this article.</span></span>

<span data-ttu-id="67af8-172">Todos os recursos do Azure que criar a rede virtual agora estão capaz de toocommunicate entre si por meio de seus endereços IP.</span><span class="sxs-lookup"><span data-stu-id="67af8-172">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="67af8-173">Se você estiver usando a resolução de nomes do Azure padrão para redes virtuais hello, Olá recursos em redes virtuais Olá não estão tooresolve capaz de nomes entre redes virtuais hello.</span><span class="sxs-lookup"><span data-stu-id="67af8-173">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="67af8-174">Se você quiser tooresolve nomes entre redes virtuais em um emparelhamento, você deve criar seu próprio servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="67af8-174">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="67af8-175">Saiba como tooset backup [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="67af8-175">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="67af8-176"><a name="cli"></a>Criar emparelhamento – CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="67af8-176"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="67af8-177">saudação de script a seguir:</span><span class="sxs-lookup"><span data-stu-id="67af8-177">hello following script:</span></span>

- <span data-ttu-id="67af8-178">Requer Olá CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="67af8-178">Requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="67af8-179">versão de hello toofind, execute Olá `az --version` comando.</span><span class="sxs-lookup"><span data-stu-id="67af8-179">toofind hello version, run hello `az --version` command.</span></span> <span data-ttu-id="67af8-180">Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67af8-180">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
- <span data-ttu-id="67af8-181">Funciona em um shell do Bash.</span><span class="sxs-lookup"><span data-stu-id="67af8-181">Works in a Bash shell.</span></span> <span data-ttu-id="67af8-182">Para obter opções sobre a execução de scripts de CLI do Azure no cliente do Windows, consulte [em execução Olá CLI do Azure no Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67af8-182">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 

<span data-ttu-id="67af8-183">Em vez de instalar hello CLI e suas dependências, você pode usar o hello Shell de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="67af8-183">Instead of installing hello CLI and its dependencies, you can use hello Azure Cloud Shell.</span></span> <span data-ttu-id="67af8-184">Olá Shell de nuvem do Azure é um shell Bash livre que podem ser executados diretamente no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="67af8-184">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="67af8-185">Ele tem Olá CLI do Azure pré-instalado e configurado toouse com sua conta.</span><span class="sxs-lookup"><span data-stu-id="67af8-185">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="67af8-186">Clique em Olá **Experimente** botão no script hello que segue, que invoca um Shell de nuvem que registra que você pode fazer logon no tooyour conta do Azure com.</span><span class="sxs-lookup"><span data-stu-id="67af8-186">Click hello **Try it** button in hello script that follows, which invokes a Cloud Shell that logs you can log in tooyour Azure account with.</span></span> <span data-ttu-id="67af8-187">tooexecute Olá script, clique em Olá **cópia** botão e cole o conteúdo de saudação em seu Shell de nuvem.</span><span class="sxs-lookup"><span data-stu-id="67af8-187">tooexecute hello script, click hello **Copy** button and paste hello contents into your Cloud Shell.</span></span>

1. <span data-ttu-id="67af8-188">Crie um grupo de recursos e duas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="67af8-188">Create a resource group and two virtual networks.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. <span data-ttu-id="67af8-189">Crie uma rede virtual emparelhamento entre duas redes virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="67af8-189">Create a virtual network peering between hello two virtual networks.</span></span>
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. <span data-ttu-id="67af8-190">Após a execução do script hello, examine emparelhamentos Olá para cada rede virtual.</span><span class="sxs-lookup"><span data-stu-id="67af8-190">After hello script executes, review hello peerings for each virtual network.</span></span> 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="67af8-191">Executar comando anterior Olá novamente, substituindo *myVnet1* com *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="67af8-191">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="67af8-192">saída de Hello dos dois comandos mostra **conectado** em Olá **PeeringState** coluna.</span><span class="sxs-lookup"><span data-stu-id="67af8-192">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>

     <span data-ttu-id="67af8-193">Todos os recursos do Azure que criar a rede virtual agora estão capaz de toocommunicate entre si por meio de seus endereços IP.</span><span class="sxs-lookup"><span data-stu-id="67af8-193">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="67af8-194">Se você estiver usando a resolução de nomes do Azure padrão para redes virtuais hello, Olá recursos em redes virtuais Olá não estão tooresolve capaz de nomes entre redes virtuais hello.</span><span class="sxs-lookup"><span data-stu-id="67af8-194">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="67af8-195">Se você quiser tooresolve nomes entre redes virtuais em um emparelhamento, você deve criar seu próprio servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="67af8-195">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="67af8-196">Saiba como tooset backup [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="67af8-196">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

4. <span data-ttu-id="67af8-197">**Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.</span><span class="sxs-lookup"><span data-stu-id="67af8-197">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
5. <span data-ttu-id="67af8-198">**Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em [excluir recursos](#delete-cli) neste artigo.</span><span class="sxs-lookup"><span data-stu-id="67af8-198">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>


## <span data-ttu-id="67af8-199"><a name="powershell"></a>Criar emparelhamento – PowerShell</span><span class="sxs-lookup"><span data-stu-id="67af8-199"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="67af8-200">Instale a versão mais recente Olá de saudação do PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo.</span><span class="sxs-lookup"><span data-stu-id="67af8-200">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="67af8-201">Se você for novo tooAzure PowerShell, consulte [visão geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67af8-201">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="67af8-202">toostart uma sessão do PowerShell, ir muito**iniciar**, digite **powershell**e, em seguida, clique em **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="67af8-202">toostart a PowerShell session, go too**Start**, enter **powershell**, and then click **PowerShell**.</span></span>
3. <span data-ttu-id="67af8-203">No PowerShell, faça logon no tooAzure digitando Olá `login-azurermaccount` comando.</span><span class="sxs-lookup"><span data-stu-id="67af8-203">In PowerShell, log in tooAzure by entering hello `login-azurermaccount` command.</span></span> <span data-ttu-id="67af8-204">conta Olá com que log deve ter Olá permissões necessárias toocreate um emparelhamento de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="67af8-204">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="67af8-205">Consulte Olá [permissões](#permissions) deste artigo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="67af8-205">See hello [Permissions](#permissions) section of this article for details.</span></span>
4. <span data-ttu-id="67af8-206">Crie um grupo de recursos e duas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="67af8-206">Create a resource group and two virtual networks.</span></span> <span data-ttu-id="67af8-207">script de saudação tooexecute, cópia Olá seguinte script, cole-o no PowerShell e pressione `Enter` após a última linha de saudação aparece na tela hello:</span><span class="sxs-lookup"><span data-stu-id="67af8-207">tooexecute hello script, copy hello following script, paste it into PowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. <span data-ttu-id="67af8-208">Crie uma rede virtual emparelhamento entre duas redes virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="67af8-208">Create a virtual network peering between hello two virtual networks.</span></span> <span data-ttu-id="67af8-209">A seguir Olá cópia script, cole em tooPowerShell e, em seguida, pressione `Enter` após a última linha de saudação aparece na tela hello:</span><span class="sxs-lookup"><span data-stu-id="67af8-209">Copy hello following script, paste in tooPowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. <span data-ttu-id="67af8-210">subredes tooreview Olá para rede virtual Olá, cópia Olá seguinte comando, cole em tooPowerShell e, em seguida, pressione `Enter`:</span><span class="sxs-lookup"><span data-stu-id="67af8-210">tooreview hello subnets for hello virtual network, copy hello following command, paste in tooPowerShell, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="67af8-211">Executar comando anterior Olá novamente, substituindo *myVnet1* com *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="67af8-211">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="67af8-212">saída de Hello dos dois comandos mostra **conectado** em Olá **PeeringState** coluna.</span><span class="sxs-lookup"><span data-stu-id="67af8-212">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>
7. <span data-ttu-id="67af8-213">**Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.</span><span class="sxs-lookup"><span data-stu-id="67af8-213">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
8. <span data-ttu-id="67af8-214">**Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em [excluir recursos](#delete-powershell) neste artigo.</span><span class="sxs-lookup"><span data-stu-id="67af8-214">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>

<span data-ttu-id="67af8-215">Todos os recursos do Azure que criar a rede virtual agora estão capaz de toocommunicate entre si por meio de seus endereços IP.</span><span class="sxs-lookup"><span data-stu-id="67af8-215">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="67af8-216">Se você estiver usando a resolução de nomes do Azure padrão para redes virtuais hello, Olá recursos em redes virtuais Olá não estão tooresolve capaz de nomes entre redes virtuais hello.</span><span class="sxs-lookup"><span data-stu-id="67af8-216">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="67af8-217">Se você quiser tooresolve nomes entre redes virtuais em um emparelhamento, você deve criar seu próprio servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="67af8-217">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="67af8-218">Saiba como tooset backup [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="67af8-218">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="67af8-219"><a name="template"></a>Criar emparelhamento – modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="67af8-219"><a name="template"></a>Create peering - Resource Manager template</span></span>

1. <span data-ttu-id="67af8-220">Consulte [Criar um emparelhamento de rede virtual](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) usando um modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="67af8-220">Reference [Create a virtual network peering](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager template.</span></span> <span data-ttu-id="67af8-221">As instruções são fornecidas com o modelo de saudação para implantar o modelo de saudação usando Olá Olá CLI do Azure, o PowerShell ou o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="67af8-221">Instructions are provided with hello template for deploying hello template using hello Azure portal, PowerShell, or hello Azure CLI.</span></span> <span data-ttu-id="67af8-222">Log na ferramenta toowhichever escolher toodeploy Olá modelo usando uma conta que tenha Olá permissões necessárias toocreate um emparelhamento de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="67af8-222">Log in toowhichever tool you choose toodeploy hello template with using an account that has hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="67af8-223">Consulte Olá [permissões](#permissions) deste artigo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="67af8-223">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="67af8-224">**Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.</span><span class="sxs-lookup"><span data-stu-id="67af8-224">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
3. <span data-ttu-id="67af8-225">**Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em Olá [excluir recursos](#delete) deste artigo, usando Olá Olá CLI do Azure, o PowerShell ou o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="67af8-225">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete) section of this article, using either hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

## <span data-ttu-id="67af8-226"><a name="permissions"></a>Permissões</span><span class="sxs-lookup"><span data-stu-id="67af8-226"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="67af8-227">contas de saudação que usar toocreate um emparelhamento de rede virtual devem ter função necessário hello ou as permissões.</span><span class="sxs-lookup"><span data-stu-id="67af8-227">hello accounts you use toocreate a virtual network peering must have hello necessary role or permissions.</span></span> <span data-ttu-id="67af8-228">Por exemplo, se foram emparelhamento duas redes virtuais, VNet1 e VNet2 de chamada, sua conta deverá ser atribuída Olá função mínimo ou as permissões para cada rede virtual a seguir:</span><span class="sxs-lookup"><span data-stu-id="67af8-228">For example, if you were peering two virtual networks named VNet1 and VNet2, your account must be assigned hello following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="67af8-229">Rede virtual</span><span class="sxs-lookup"><span data-stu-id="67af8-229">Virtual network</span></span>|<span data-ttu-id="67af8-230">Função</span><span class="sxs-lookup"><span data-stu-id="67af8-230">Role</span></span>|<span data-ttu-id="67af8-231">Permissões</span><span class="sxs-lookup"><span data-stu-id="67af8-231">Permissions</span></span>|
|---|---|---|
|<span data-ttu-id="67af8-232">VNet1</span><span class="sxs-lookup"><span data-stu-id="67af8-232">VNet1</span></span>|[<span data-ttu-id="67af8-233">Colaborador de rede</span><span class="sxs-lookup"><span data-stu-id="67af8-233">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="67af8-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="67af8-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
|<span data-ttu-id="67af8-235">VNet2</span><span class="sxs-lookup"><span data-stu-id="67af8-235">VNet2</span></span>|[<span data-ttu-id="67af8-236">Colaborador de rede</span><span class="sxs-lookup"><span data-stu-id="67af8-236">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="67af8-237">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="67af8-237">Microsoft.Network/virtualNetworks/peer</span></span>|

<span data-ttu-id="67af8-238">Saiba mais sobre [funções internas](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) e atribuindo permissões específicas muito[funções personalizadas](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (somente no Gerenciador de recursos).</span><span class="sxs-lookup"><span data-stu-id="67af8-238">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions too[custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="67af8-239"><a name="delete"></a>Excluir recursos</span><span class="sxs-lookup"><span data-stu-id="67af8-239"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="67af8-240">Quando concluir este tutorial, você pode desejar que recursos de saudação toodelete criado no tutorial hello, portanto você não incorrer em encargos de uso.</span><span class="sxs-lookup"><span data-stu-id="67af8-240">When you've finished this tutorial, you might want toodelete hello resources you created in hello tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="67af8-241">Excluir um grupo de recursos também exclui todos os recursos que estão no grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="67af8-241">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="67af8-242"><a name="delete-portal"></a>Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="67af8-242"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="67af8-243">Na caixa de pesquisa do portal hello, insira **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="67af8-243">In hello portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="67af8-244">Nos resultados da pesquisa de saudação, clique em **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="67af8-244">In hello search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="67af8-245">Em Olá **myResourceGroup** folha, clique em Olá **excluir** ícone.</span><span class="sxs-lookup"><span data-stu-id="67af8-245">On hello **myResourceGroup** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="67af8-246">tooconfirm Olá exclusão, Olá **Olá tipo nome do grupo de recursos** , digite **myResourceGroup**e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="67af8-246">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="67af8-247"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="67af8-247"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="67af8-248">Digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="67af8-248">Enter hello following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="67af8-249"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="67af8-249"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="67af8-250">Digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="67af8-250">Enter hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a><span data-ttu-id="67af8-251">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="67af8-251">Next steps</span></span>

- <span data-ttu-id="67af8-252">Familiarize por completo com [comportamentos e restrições importantes do emparelhamento de rede virtual](virtual-network-manage-peering.md#requirements-and-constraints) antes de criar um emparelhamento de rede virtual para uso em produção.</span><span class="sxs-lookup"><span data-stu-id="67af8-252">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="67af8-253">Saiba mais sobre todas as [configurações de emparelhamento de rede virtual](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="67af8-253">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="67af8-254">Saiba como muito[criar um hub e spoke de topologia de rede](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) com o emparelhamento de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="67af8-254">Learn how too[create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
