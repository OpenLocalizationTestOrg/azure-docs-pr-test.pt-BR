---
title: Gerenciar NSGs usando o portal do Azure | Microsoft Docs
description: Saiba como gerenciar NSGs existentes usando o Portal do Azure.
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
ms.openlocfilehash: e9bcf8a893ff209337f6a5763b631a22f8514e20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-nsgs-using-the-portal"></a><span data-ttu-id="9c890-103">Gerenciar NSGs usando o portal</span><span class="sxs-lookup"><span data-stu-id="9c890-103">Manage NSGs using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c890-104">Portal</span><span class="sxs-lookup"><span data-stu-id="9c890-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="9c890-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c890-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="9c890-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9c890-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="9c890-107">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9c890-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9c890-108">Este artigo aborda usando o modelo de implantação do Gerenciador de Recursos, que a Microsoft recomenda para a maioria das novas implantações em vez de do modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="9c890-108">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="9c890-109">Recuperar informações</span><span class="sxs-lookup"><span data-stu-id="9c890-109">Retrieve Information</span></span>
<span data-ttu-id="9c890-110">Você pode exibir seus NSGs existentes, recuperar regras para um NSG existente e descobrir a quais recursos um NSG está associado.</span><span class="sxs-lookup"><span data-stu-id="9c890-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="9c890-111">Exibir NSGs existentes</span><span class="sxs-lookup"><span data-stu-id="9c890-111">View existing NSGs</span></span>

<span data-ttu-id="9c890-112">Para exibir todos os NSGs existentes em uma assinatura, siga as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="9c890-112">To view all existing NSGs in a subscription, complete the following steps:</span></span>

1. <span data-ttu-id="9c890-113">Em um navegador, navegue até http://portal.azure.com e, se necessário, entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c890-113">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="9c890-114">Clique em **Procurar >** > **Grupos de segurança de rede**.</span><span class="sxs-lookup"><span data-stu-id="9c890-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="9c890-116">Verifique a lista de NSGs na folha **Grupos de segurança de rede** .</span><span class="sxs-lookup"><span data-stu-id="9c890-116">Check the list of NSGs in the **Network security groups** blade.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="9c890-118">Exibir NSGs em um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="9c890-118">View NSGs in a resource group</span></span>

<span data-ttu-id="9c890-119">Para exibir a lista de NSGs no grupo de recursos **RG-NSG**, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c890-119">To view the list of NSGs in the **RG-NSG** resource group, complete the following steps:</span></span>

1. <span data-ttu-id="9c890-120">Clique em **Grupos de recursos >** > **RG-NSG** > **...**.</span><span class="sxs-lookup"><span data-stu-id="9c890-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="9c890-122">Na lista de recursos, procure itens que exibam o ícone do NSG, conforme mostrado na folha **Recursos** abaixo.</span><span class="sxs-lookup"><span data-stu-id="9c890-122">In the list of resources, look for items displaying the NSG icon, as shown in the **Resources** blade below.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="9c890-124">Listar todas as regras de um NSG</span><span class="sxs-lookup"><span data-stu-id="9c890-124">List all rules for an NSG</span></span>

<span data-ttu-id="9c890-125">Para exibir as regras de um NSG chamado **NSG-FrontEnd**, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c890-125">To view the rules of an NSG named **NSG-FrontEnd**, complete the following steps:</span></span>

1. <span data-ttu-id="9c890-126">Na folha **Grupos de segurança de rede**, ou na folha **Recursos** mostrada acima, clique em **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="9c890-126">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="9c890-127">Na guia **Configurações**, clique em **Regras de segurança de entrada**.</span><span class="sxs-lookup"><span data-stu-id="9c890-127">In the **Settings** tab, click **Inbound security rules**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="9c890-129">A folha **Regras de segurança de entrada** é exibida como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="9c890-129">The **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="9c890-131">Na guia **Configurações**, clique em **Regras de segurança de saída** para ver as regras de saída.</span><span class="sxs-lookup"><span data-stu-id="9c890-131">In the **Settings** tab, click **Outbound security rules** to see the outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9c890-132">Para exibir as regras padrão, clique no ícone **Regras padrão** , na parte superior da folha que exibe as regras.</span><span class="sxs-lookup"><span data-stu-id="9c890-132">To view default rules, click the **Default rules** icon at the top of the blade that displays the rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="9c890-133">Exibir associações de NSGs</span><span class="sxs-lookup"><span data-stu-id="9c890-133">View NSGs associations</span></span>

<span data-ttu-id="9c890-134">Para ver a quais recursos o NSG **NSG-FrontEnd** está associado, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c890-134">To view what resources the **NSG-FrontEnd** NSG is associate with, complete the following steps:</span></span>

1. <span data-ttu-id="9c890-135">Na folha **Grupos de segurança de rede**, ou na folha **Recursos** mostrada acima, clique em **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="9c890-135">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="9c890-136">Na guia **Configurações**, clique em **Sub-redes** para ver quais sub-redes estão associadas ao NSG.</span><span class="sxs-lookup"><span data-stu-id="9c890-136">In the **Settings** tab, click **Subnets** to view what subnets are associated to the NSG.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="9c890-138">Na guia **Configurações**, clique em **adaptadores de rede** para ver quais NICs estão associadas ao NSG.</span><span class="sxs-lookup"><span data-stu-id="9c890-138">In the **Settings** tab, click **Network interfaces** to view what NICs are associated to the NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="9c890-139">Gerenciar regras</span><span class="sxs-lookup"><span data-stu-id="9c890-139">Manage rules</span></span>
<span data-ttu-id="9c890-140">Você pode adicionar regras a um NSG existente, editar regras existentes e remover regras.</span><span class="sxs-lookup"><span data-stu-id="9c890-140">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="9c890-141">Adicionar uma regra</span><span class="sxs-lookup"><span data-stu-id="9c890-141">Add a rule</span></span>
<span data-ttu-id="9c890-142">Para adicionar uma regra permitindo o tráfego de **entrada** na porta **443** de qualquer computador para o NSG **NSG-FrontEnd**, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c890-142">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="9c890-143">Na folha **Grupos de segurança de rede**, ou na folha **Recursos** mostrada acima, clique em **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="9c890-143">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="9c890-144">Na guia **Configurações**, clique em **Regras de segurança de entrada**.</span><span class="sxs-lookup"><span data-stu-id="9c890-144">In the **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="9c890-145">Na folha **Regras de segurança de entrada**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9c890-145">In the **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="9c890-146">Na folha **Adicionar regra de segurança de entrada**, preencha os valores como mostrado abaixo e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9c890-146">Then, in the **Add inbound security rule** blade, fill the values as shown below, and then click **OK**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="9c890-148">Depois de alguns segundos, observe a nova regra na folha **Regras de segurança de entrada** .</span><span class="sxs-lookup"><span data-stu-id="9c890-148">After a few seconds, notice the new rule in the **Inbound security rules** blade.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="9c890-150">Alterar uma regra</span><span class="sxs-lookup"><span data-stu-id="9c890-150">Change a rule</span></span>
<span data-ttu-id="9c890-151">Para alterar a regra criada acima para permitir o tráfego de entrada apenas da **Internet**, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c890-151">To change the rule created above to allow inbound traffic from the **Internet** only, complete the following steps:</span></span>

1. <span data-ttu-id="9c890-152">Na folha **Grupos de segurança de rede**, ou na folha **Recursos** mostrada acima, clique em **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="9c890-152">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="9c890-153">Na guia **Configurações** , clique na regra criada acima.</span><span class="sxs-lookup"><span data-stu-id="9c890-153">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="9c890-154">Na folha **allow-https**, altere a propriedade **Source** como mostrado abaixo e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9c890-154">In the **allow-https** blade, change the **Source** property as shown below, and then click **Save**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="9c890-156">Excluir uma regra</span><span class="sxs-lookup"><span data-stu-id="9c890-156">Delete a rule</span></span>

<span data-ttu-id="9c890-157">Para excluir a regra criada anteriormente, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9c890-157">To delete the rule created above, complete the following steps:</span></span>

1. <span data-ttu-id="9c890-158">Na folha **Grupos de segurança de rede**, ou na folha **Recursos** mostrada acima, clique em **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="9c890-158">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="9c890-159">Na guia **Configurações** , clique na regra criada acima.</span><span class="sxs-lookup"><span data-stu-id="9c890-159">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="9c890-160">Na folha **allow-https**, clique em **Excluir** e em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="9c890-160">In the **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="9c890-162">Gerenciar associações</span><span class="sxs-lookup"><span data-stu-id="9c890-162">Manage associations</span></span>
<span data-ttu-id="9c890-163">É possível associar um NSG a sub-redes e NICs.</span><span class="sxs-lookup"><span data-stu-id="9c890-163">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="9c890-164">Você também pode desassociar um NSG de qualquer recurso ao qual ele esteja associado.</span><span class="sxs-lookup"><span data-stu-id="9c890-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="9c890-165">Associar um NSG a uma NIC</span><span class="sxs-lookup"><span data-stu-id="9c890-165">Associate an NSG to a NIC</span></span>
<span data-ttu-id="9c890-166">Para associar o NSG **NSG-FrontEnd** à NIC **TestNICWeb1**, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c890-166">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="9c890-167">Na folha **Grupos de segurança de rede**, ou na folha **Recursos** mostrada acima, clique em **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="9c890-167">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="9c890-168">Na guia **configurações**, clique em **Adaptadores de rede** > **Associar** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="9c890-168">In the **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="9c890-170">Desassociar um NSG de uma NIC</span><span class="sxs-lookup"><span data-stu-id="9c890-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="9c890-171">Para desassociar o NSG **NSG-FrontEnd** da NIC **TestNICWeb1**, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c890-171">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="9c890-172">No portal do Azure, clique em **Grupos de recursos>** > **RG-NSG** > **...** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="9c890-172">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="9c890-173">Na folha **TestNICWeb1**, clique em **Alterar segurança...** > **Nenhum**.</span><span class="sxs-lookup"><span data-stu-id="9c890-173">In the **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="9c890-175">Você também pode usar essa folha para associar a NIC a qualquer NSG existente.</span><span class="sxs-lookup"><span data-stu-id="9c890-175">You can also use this blade to associate the NIC to any existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="9c890-176">Desassociar um NSG de uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="9c890-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="9c890-177">Para desassociar o NSG **NSG-FrontEnd** da sub-rede **FrontEnd**, siga as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9c890-177">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="9c890-178">No portal do Azure, clique em **Grupos de recursos >** > **RG-NSG** > **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="9c890-178">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="9c890-179">Na folha **Configurações**, clique em **Sub-redes** > **FrontEnd** > **Grupo de segurança de rede** > **Nenhum**.</span><span class="sxs-lookup"><span data-stu-id="9c890-179">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="9c890-181">Na folha **FrontEnd**, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9c890-181">In the **FrontEnd** blade, click **Save**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="9c890-183">Associar um NSG a uma sub-rede</span><span class="sxs-lookup"><span data-stu-id="9c890-183">Associate an NSG to a subnet</span></span>

<span data-ttu-id="9c890-184">Para associar o NSG **NSG-FrontEnd** à sub-rede **FronEnd** novamente, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c890-184">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="9c890-185">No portal do Azure, clique em **Grupos de recursos >** > **RG-NSG** > **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="9c890-185">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="9c890-186">Na folha **Configurações**, clique em **Sub-redes** > **FrontEnd** > **Grupo de segurança de rede** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="9c890-186">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="9c890-187">Na folha **FrontEnd**, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="9c890-187">In the **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="9c890-188">Você também pode associar um NSG a uma sub-rede na folha **Configurações** do NSG.</span><span class="sxs-lookup"><span data-stu-id="9c890-188">You can also associate an NSG to a subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="9c890-189">Excluir um NSG</span><span class="sxs-lookup"><span data-stu-id="9c890-189">Delete an NSG</span></span>
<span data-ttu-id="9c890-190">Você pode excluir um NSG apenas se ele não estiver associado a nenhum recurso.</span><span class="sxs-lookup"><span data-stu-id="9c890-190">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="9c890-191">Para excluir um NSG, conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="9c890-191">To delete an NSG, complete the following steps:.</span></span>

1. <span data-ttu-id="9c890-192">No portal do Azure, clique em **Grupos de recursos >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="9c890-192">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="9c890-193">Na folha **Configurações**, clique em **Adaptadores de rede**.</span><span class="sxs-lookup"><span data-stu-id="9c890-193">In the **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="9c890-194">Se houver alguma NIC listada, clique na NIC e siga a etapa 2 em [Desassociar um NSG de uma NIC](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="9c890-194">If there are any NICs listed, click the NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="9c890-195">Repita a etapa 3 para cada NIC.</span><span class="sxs-lookup"><span data-stu-id="9c890-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="9c890-196">Na folha **Configurações**, clique em **Sub-redes**.</span><span class="sxs-lookup"><span data-stu-id="9c890-196">In the **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="9c890-197">Se houver alguma sub-rede listada, clique na sub-rede e siga as etapas 2 e 3 em [Desassociar um NSG de uma sub-rede](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="9c890-197">If there are any subnets listed, click the subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="9c890-198">Role da esquerda para a folha **NSG-FrontEnd** e clique em **Excluir** > **Sim**.</span><span class="sxs-lookup"><span data-stu-id="9c890-198">Scrolls left to the **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Portal do Azure - NSGs](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="9c890-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9c890-200">Next steps</span></span>
* <span data-ttu-id="9c890-201">[Habilitar registro em log](virtual-network-nsg-manage-log.md) para NSGs.</span><span class="sxs-lookup"><span data-stu-id="9c890-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
