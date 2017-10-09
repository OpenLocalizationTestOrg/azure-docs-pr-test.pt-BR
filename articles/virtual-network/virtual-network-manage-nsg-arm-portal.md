---
title: "aaaManage NSGs usando Olá portal do Azure | Microsoft Docs"
description: "Saiba como toomanage existente NSGs usando Olá portal do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a><span data-ttu-id="05969-103">Gerenciar os NSGs usando o portal de saudação</span><span class="sxs-lookup"><span data-stu-id="05969-103">Manage NSGs using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="05969-104">Portal</span><span class="sxs-lookup"><span data-stu-id="05969-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="05969-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="05969-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="05969-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="05969-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="05969-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="05969-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="05969-108">Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez do modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="05969-108">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="05969-109">Recuperar informações</span><span class="sxs-lookup"><span data-stu-id="05969-109">Retrieve Information</span></span>
<span data-ttu-id="05969-110">Você pode exibir seus NSGs existentes, recuperar regras para um NSG existente e descobrir a quais recursos um NSG está associado.</span><span class="sxs-lookup"><span data-stu-id="05969-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="05969-111">Exibir NSGs existentes</span><span class="sxs-lookup"><span data-stu-id="05969-111">View existing NSGs</span></span>

<span data-ttu-id="05969-112">tooview todos os existentes NSGs em uma assinatura, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="05969-112">tooview all existing NSGs in a subscription, complete hello following steps:</span></span>

1. <span data-ttu-id="05969-113">Em um navegador, navegue toohttp://portal.azure.com e, se necessário, entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="05969-113">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="05969-114">Clique em **Procurar >** > **Grupos de segurança de rede**.</span><span class="sxs-lookup"><span data-stu-id="05969-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="05969-116">Verifique a lista de saudação do NSGs em hello **grupos de segurança de rede** folha.</span><span class="sxs-lookup"><span data-stu-id="05969-116">Check hello list of NSGs in hello **Network security groups** blade.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="05969-118">Exibir NSGs em um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="05969-118">View NSGs in a resource group</span></span>

<span data-ttu-id="05969-119">lista de saudação do tooview de NSGs em Olá **NSG RG** grupo de recursos, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="05969-119">tooview hello list of NSGs in hello **RG-NSG** resource group, complete hello following steps:</span></span>

1. <span data-ttu-id="05969-120">Clique em **Grupos de recursos >** > **RG-NSG** > **...**.</span><span class="sxs-lookup"><span data-stu-id="05969-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="05969-122">Na lista de saudação de recursos, observe para itens de exibição de ícone do NSG hello, conforme mostrado no hello **recursos** folha abaixo.</span><span class="sxs-lookup"><span data-stu-id="05969-122">In hello list of resources, look for items displaying hello NSG icon, as shown in hello **Resources** blade below.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="05969-124">Listar todas as regras de um NSG</span><span class="sxs-lookup"><span data-stu-id="05969-124">List all rules for an NSG</span></span>

<span data-ttu-id="05969-125">regras de saudação tooview de um NSG denominado **NSG-front-end**completa Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="05969-125">tooview hello rules of an NSG named **NSG-FrontEnd**, complete hello following steps:</span></span>

1. <span data-ttu-id="05969-126">De saudação **grupos de segurança de rede** folha ou hello **recursos** folha mostrada acima, clique em **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="05969-126">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="05969-127">Em Olá **configurações** , clique em **regras de segurança de entrada**.</span><span class="sxs-lookup"><span data-stu-id="05969-127">In hello **Settings** tab, click **Inbound security rules**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="05969-129">Olá **regras de segurança de entrada** folha é exibida conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="05969-129">hello **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="05969-131">Em Olá **configurações** , clique em **regras de segurança de saída** toosee Olá regras de saída.</span><span class="sxs-lookup"><span data-stu-id="05969-131">In hello **Settings** tab, click **Outbound security rules** toosee hello outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="05969-132">tooview regras do padrão, clique em Olá **padrão regras** no hello superior da folha de saudação que exibe as regras de saudação.</span><span class="sxs-lookup"><span data-stu-id="05969-132">tooview default rules, click hello **Default rules** icon at hello top of hello blade that displays hello rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="05969-133">Exibir associações de NSGs</span><span class="sxs-lookup"><span data-stu-id="05969-133">View NSGs associations</span></span>

<span data-ttu-id="05969-134">tooview Olá quais recursos **NSG-front-end** NSG está associado ao e completa Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="05969-134">tooview what resources hello **NSG-FrontEnd** NSG is associate with, complete hello following steps:</span></span>

1. <span data-ttu-id="05969-135">De saudação **grupos de segurança de rede** folha ou hello **recursos** folha mostrada acima, clique em **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="05969-135">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="05969-136">Em Olá **configurações** , clique em **sub-redes** tooview que sub-redes são associados toohello NSG.</span><span class="sxs-lookup"><span data-stu-id="05969-136">In hello **Settings** tab, click **Subnets** tooview what subnets are associated toohello NSG.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="05969-138">Em Olá **configurações** , clique em **interfaces de rede** tooview quais NICs são associados toohello NSG.</span><span class="sxs-lookup"><span data-stu-id="05969-138">In hello **Settings** tab, click **Network interfaces** tooview what NICs are associated toohello NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="05969-139">Gerenciar regras</span><span class="sxs-lookup"><span data-stu-id="05969-139">Manage rules</span></span>
<span data-ttu-id="05969-140">Você pode adicionar regras tooan existente NSG, editar regras existentes e remova regras.</span><span class="sxs-lookup"><span data-stu-id="05969-140">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="05969-141">Adicionar uma regra</span><span class="sxs-lookup"><span data-stu-id="05969-141">Add a rule</span></span>
<span data-ttu-id="05969-142">tooadd uma regra permitindo **entrada** tráfego tooport **443** de qualquer máquina toohello **NSG-front-end** NSG, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="05969-142">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="05969-143">De saudação **grupos de segurança de rede** folha ou hello **recursos** folha mostrada acima, clique em **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="05969-143">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="05969-144">Em Olá **configurações** , clique em **regras de segurança de entrada**.</span><span class="sxs-lookup"><span data-stu-id="05969-144">In hello **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="05969-145">Em Olá **regras de segurança de entrada** folha, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="05969-145">In hello **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="05969-146">Em seguida, no hello **Adicionar regra de segurança de entrada** folha, preencher valores hello, conforme mostrado abaixo e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="05969-146">Then, in hello **Add inbound security rule** blade, fill hello values as shown below, and then click **OK**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="05969-148">Depois de alguns segundos, observe a nova regra Olá no hello **regras de segurança de entrada** folha.</span><span class="sxs-lookup"><span data-stu-id="05969-148">After a few seconds, notice hello new rule in hello **Inbound security rules** blade.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="05969-150">Alterar uma regra</span><span class="sxs-lookup"><span data-stu-id="05969-150">Change a rule</span></span>
<span data-ttu-id="05969-151">regra de saudação toochange criada acima tooallow Olá o tráfego de entrada **Internet** Olá completa, somente as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="05969-151">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, complete hello following steps:</span></span>

1. <span data-ttu-id="05969-152">De saudação **grupos de segurança de rede** folha ou hello **recursos** folha mostrada acima, clique em **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="05969-152">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="05969-153">Em Olá **configurações** , clique em regra Olá criada acima.</span><span class="sxs-lookup"><span data-stu-id="05969-153">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="05969-154">Em Olá **https permitir** folha, alteração Olá **fonte** propriedade conforme mostrado abaixo e depois clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="05969-154">In hello **allow-https** blade, change hello **Source** property as shown below, and then click **Save**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="05969-156">Excluir uma regra</span><span class="sxs-lookup"><span data-stu-id="05969-156">Delete a rule</span></span>

<span data-ttu-id="05969-157">toodelete Olá regra criada acima e completa Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="05969-157">toodelete hello rule created above, complete hello following steps:</span></span>

1. <span data-ttu-id="05969-158">De saudação **grupos de segurança de rede** folha ou hello **recursos** folha mostrada acima, clique em **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="05969-158">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="05969-159">Em Olá **configurações** , clique em regra Olá criada acima.</span><span class="sxs-lookup"><span data-stu-id="05969-159">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="05969-160">Em Olá **https permitir** folha, clique em **excluir**e, em seguida, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="05969-160">In hello **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="05969-162">Gerenciar associações</span><span class="sxs-lookup"><span data-stu-id="05969-162">Manage associations</span></span>
<span data-ttu-id="05969-163">Você pode associar um NSG toosubnets e placas de rede.</span><span class="sxs-lookup"><span data-stu-id="05969-163">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="05969-164">Você também pode desassociar um NSG de qualquer recurso ao qual ele esteja associado.</span><span class="sxs-lookup"><span data-stu-id="05969-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="05969-165">Associar um NSG tooa NIC</span><span class="sxs-lookup"><span data-stu-id="05969-165">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="05969-166">Olá tooassociate **NSG-front-end** NSG toohello **TestNICWeb1** NIC, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="05969-166">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="05969-167">De saudação **grupos de segurança de rede** folha ou hello **recursos** folha mostrada acima, clique em **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="05969-167">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="05969-168">Em Olá **configurações** , clique em **interfaces de rede** > **associar** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="05969-168">In hello **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="05969-170">Desassociar um NSG de uma NIC</span><span class="sxs-lookup"><span data-stu-id="05969-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="05969-171">Olá toodissociate **NSG-front-end** NSG de saudação **TestNICWeb1** NIC, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="05969-171">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="05969-172">De Olá portal do Azure, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="05969-172">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="05969-173">Em Olá **TestNICWeb1** folha, clique em **alterar a segurança...**   >  **Nenhum**.</span><span class="sxs-lookup"><span data-stu-id="05969-173">In hello **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="05969-175">Você também pode usar esta folha tooassociate Olá NIC tooany, existente NSG.</span><span class="sxs-lookup"><span data-stu-id="05969-175">You can also use this blade tooassociate hello NIC tooany existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="05969-176">Desassociar um NSG de uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="05969-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="05969-177">Olá toodissociate **NSG-front-end** NSG de saudação **front-end** sub-rede, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="05969-177">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="05969-178">De Olá portal do Azure, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="05969-178">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="05969-179">Em Olá **configurações** folha, clique em **sub-redes** > **front-end** > **grupo de segurança de rede**  >  **Nenhum**.</span><span class="sxs-lookup"><span data-stu-id="05969-179">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="05969-181">Em Olá **front-end** folha, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="05969-181">In hello **FrontEnd** blade, click **Save**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="05969-183">Associar uma sub-rede de tooa NSG</span><span class="sxs-lookup"><span data-stu-id="05969-183">Associate an NSG tooa subnet</span></span>

<span data-ttu-id="05969-184">Olá tooassociate **NSG-front-end** NSG toohello **FronEnd** sub-rede novamente, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="05969-184">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="05969-185">De Olá portal do Azure, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="05969-185">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="05969-186">Em Olá **configurações** folha, clique em **sub-redes** > **front-end** > **grupo de segurança de rede**  >  **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="05969-186">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="05969-187">Em Olá **front-end** folha, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="05969-187">In hello **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="05969-188">Você também pode associar uma sub-rede de tooa NSG de thh NSG **configurações** folha.</span><span class="sxs-lookup"><span data-stu-id="05969-188">You can also associate an NSG tooa subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="05969-189">Excluir um NSG</span><span class="sxs-lookup"><span data-stu-id="05969-189">Delete an NSG</span></span>
<span data-ttu-id="05969-190">Você só pode excluir um NSG se ela não está associada tooany recursos.</span><span class="sxs-lookup"><span data-stu-id="05969-190">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="05969-191">toodelete um NSG, Olá concluir as etapas a seguir:.</span><span class="sxs-lookup"><span data-stu-id="05969-191">toodelete an NSG, complete hello following steps:.</span></span>

1. <span data-ttu-id="05969-192">De Olá portal do Azure, clique em **grupos de recursos >** > **RG NSG** > **...**   >  **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="05969-192">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="05969-193">Em Olá **configurações** folha, clique em **interfaces de rede**.</span><span class="sxs-lookup"><span data-stu-id="05969-193">In hello **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="05969-194">Se houver qualquer NICs listadas, clique Olá NIC e siga a etapa 2 [dissociar um NSG de uma NIC](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="05969-194">If there are any NICs listed, click hello NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="05969-195">Repita a etapa 3 para cada NIC.</span><span class="sxs-lookup"><span data-stu-id="05969-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="05969-196">Em Olá **configurações** folha, clique em **sub-redes**.</span><span class="sxs-lookup"><span data-stu-id="05969-196">In hello **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="05969-197">Se não houver nenhuma sub-rede listada, clique em sub-rede hello e siga as etapas 2 e 3 em [dissociar um NSG de uma sub-rede](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="05969-197">If there are any subnets listed, click hello subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="05969-198">Rola esquerdo toohello **NSG-front-end** folha, em seguida, clique em **excluir** > **Sim**.</span><span class="sxs-lookup"><span data-stu-id="05969-198">Scrolls left toohello **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="05969-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="05969-200">Next steps</span></span>
* <span data-ttu-id="05969-201">[Habilitar registro em log](virtual-network-nsg-manage-log.md) para NSGs.</span><span class="sxs-lookup"><span data-stu-id="05969-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
