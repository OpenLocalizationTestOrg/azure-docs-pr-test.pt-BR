---
title: "grupos de segurança de rede aaaManage - portal do Azure | Microsoft Docs"
description: "Saiba como grupos de segurança de rede toomanage usando Olá portal do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: faee5ac8-f4c4-4f97-ade5-197a37aad496
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53fb29e60cbc2a535f6cf03e430d9e703e97b216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-portal"></a><span data-ttu-id="07e9c-103">Gerenciar grupos de segurança de rede usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="07e9c-103">Manage network security groups using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="07e9c-104">Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="07e9c-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="07e9c-105">Você também pode [criar NSGs no modelo de implantação clássico Olá](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="07e9c-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="07e9c-106">exemplo Hello PowerShell comandos abaixo esperam um ambiente simples já foi criado com base no cenário de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="07e9c-106">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="07e9c-107">Se você quiser comandos de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste Olá implantando [este modelo](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), clique em **implantar tooAzure**, substitua os valores de parâmetro padrão Olá Se necessário e siga as instruções de saudação em Olá portal.</span><span class="sxs-lookup"><span data-stu-id="07e9c-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span> <span data-ttu-id="07e9c-108">Olá etapas a seguir use **NSG RG** como nome de saudação do modelo de saudação de grupo de recursos Olá foi implantada.</span><span class="sxs-lookup"><span data-stu-id="07e9c-108">hello steps below use **RG-NSG** as hello name of hello resource group hello template was deployed to.</span></span>

## <a name="create-hello-nsg-frontend-nsg"></a><span data-ttu-id="07e9c-109">Criar hello NSG NSG-front-end</span><span class="sxs-lookup"><span data-stu-id="07e9c-109">Create hello NSG-FrontEnd NSG</span></span>
<span data-ttu-id="07e9c-110">Olá toocreate **NSG-front-end** NSG conforme mostrado no cenário de saudação acima, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="07e9c-110">toocreate hello **NSG-FrontEnd** NSG as shown in hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="07e9c-111">Em um navegador, navegue toohttp://portal.azure.com e, se necessário, entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="07e9c-111">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="07e9c-112">Clique em **Procurar >** > **Grupos de segurança de rede**.</span><span class="sxs-lookup"><span data-stu-id="07e9c-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Portal do Azure - NSGs](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="07e9c-114">Em Olá **grupos de segurança de rede** folha, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="07e9c-114">In hello **Network security groups** blade, click **Add**.</span></span>
   
    ![Portal do Azure - NSGs](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="07e9c-116">Em Olá **criar grupo de segurança de rede** folha, criar um NSG denominado *NSG-front-end* em Olá *RG NSG* grupo de recursos e depois clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="07e9c-116">In hello **Create network security group** blade, create an NSG named *NSG-FrontEnd* in hello *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Portal do Azure - NSGs](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="07e9c-118">Criar regras em um NSG existente</span><span class="sxs-lookup"><span data-stu-id="07e9c-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="07e9c-119">regras de toocreate em um NSG existente da saudação portal do Azure, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="07e9c-119">toocreate rules in an existing NSG from hello Azure portal, follow hello steps below.</span></span>

1. <span data-ttu-id="07e9c-120">Clique em **Procurar >** > **Grupos de segurança de rede**.</span><span class="sxs-lookup"><span data-stu-id="07e9c-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="07e9c-121">Na lista de saudação do NSGs, clique em **NSG-front-end** > **regras de segurança de entrada**</span><span class="sxs-lookup"><span data-stu-id="07e9c-121">In hello list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Portal do Azure - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="07e9c-123">Na lista de saudação do **regras de segurança de entrada**, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="07e9c-123">In hello list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Portal do Azure - Adicionar regra](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="07e9c-125">Em Olá **Adicionar regra de segurança de entrada** folha, criar uma regra denominada *web regra* com prioridade de *200* permitindo o acesso por meio de *TCP* tooport *80* tooany VM de qualquer fonte e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="07e9c-125">In hello **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* tooport *80* tooany VM from any source, and then click **OK**.</span></span> <span data-ttu-id="07e9c-126">Observe como a maioria destas configurações já é o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="07e9c-126">Notice that most of these settings are default values already.</span></span>
   
    ![Portal do Azure - Configurações de regra](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="07e9c-128">Depois de alguns segundos, você verá a nova regra Olá no hello NSG.</span><span class="sxs-lookup"><span data-stu-id="07e9c-128">After a few seconds you will see hello new rule in hello NSG.</span></span>
   
    ![Portal do Azure - Nova regra](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="07e9c-130">Repita as etapas too6 toocreate uma regra de entrada denominada *regra rdp* com uma prioridade de *250* permitindo o acesso por meio de *TCP* tooport *3389* tooany VM de qualquer fonte.</span><span class="sxs-lookup"><span data-stu-id="07e9c-130">Repeat steps  too6 toocreate an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* tooport *3389* tooany VM from any source.</span></span>

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a><span data-ttu-id="07e9c-131">Associar Olá NSG toohello front-end sub-rede</span><span class="sxs-lookup"><span data-stu-id="07e9c-131">Associate hello NSG toohello FrontEnd subnet</span></span>
1. <span data-ttu-id="07e9c-132">Clique em **Procurar >** > **Grupos de recursos** > **RG-NSG**.</span><span class="sxs-lookup"><span data-stu-id="07e9c-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="07e9c-133">Em Olá **RG NSG** folha, clique em **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="07e9c-133">In hello **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Portal do Azure - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="07e9c-135">Em Olá **configurações** folha, clique em **sub-redes** > **front-end** > **grupo de segurança de rede**  >  **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="07e9c-135">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Portal do Azure - Configurações de sub-rede](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="07e9c-137">Em Olá **front-end** folha, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="07e9c-137">In hello **FrontEnd** blade, click **Save**.</span></span>
   
    ![Portal do Azure - Configurações de sub-rede](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a><span data-ttu-id="07e9c-139">Criar hello back-end NSG NSG</span><span class="sxs-lookup"><span data-stu-id="07e9c-139">Create hello NSG-BackEnd NSG</span></span>
<span data-ttu-id="07e9c-140">Olá toocreate **back-end NSG** NSG e associá-la toohello **back-end** sub-rede, siga Olá etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="07e9c-140">toocreate hello **NSG-BackEnd** NSG and associate it toohello **BackEnd** subnet, follow hello steps below.</span></span>

1. <span data-ttu-id="07e9c-141">Olá Repita as etapas em [criar hello FrontEnd NSG NSG](#Create-the-NSG-FrontEnd-NSG) toocreate um NSG denominado *back-end NSG*</span><span class="sxs-lookup"><span data-stu-id="07e9c-141">Repeat hello steps in [Create hello NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) toocreate an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="07e9c-142">Olá Repita as etapas em [criar regras em um NSG existente](#Create-rules-in-an-existing-NSG) toocreate Olá **entrada** regras na tabela de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="07e9c-142">Repeat hello steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) toocreate hello **inbound** rules in hello table below.</span></span>
   
   | <span data-ttu-id="07e9c-143">Regra de entrada</span><span class="sxs-lookup"><span data-stu-id="07e9c-143">Inbound rule</span></span> | <span data-ttu-id="07e9c-144">Regra de saída</span><span class="sxs-lookup"><span data-stu-id="07e9c-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Portal do Azure - regra de entrada](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Portal do Azure - regra de saída](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="07e9c-147">Olá Repita as etapas em [associar sub-rede front-end do hello NSG toohello](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate Olá **back-end NSG** NSG toohello **back-end** sub-rede.</span><span class="sxs-lookup"><span data-stu-id="07e9c-147">Repeat hello steps in [Associate hello NSG toohello FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG-Backend** NSG toohello **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07e9c-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07e9c-148">Next Steps</span></span>
* <span data-ttu-id="07e9c-149">Saiba como muito[gerenciar NSGs existentes](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="07e9c-149">Learn how too[manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="07e9c-150">[Habilite o registro em log](virtual-network-nsg-manage-log.md) para NSGs.</span><span class="sxs-lookup"><span data-stu-id="07e9c-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

