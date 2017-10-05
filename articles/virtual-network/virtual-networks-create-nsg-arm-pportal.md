---
title: "Criar grupos de segurança de rede – Portal do Azure | Microsoft Docs"
description: "Aprenda a criar e implantar grupos de segurança de rede usando o Portal do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5bc8fc2e-1e81-40e2-8231-0484cd5605cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 865032f350735d35668bb199ccf1ef3f0fae81de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-portal"></a><span data-ttu-id="398fd-103">Criar grupos de segurança de rede usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="398fd-103">Create network security groups using the Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="398fd-104">Este artigo aborda o modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="398fd-104">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="398fd-105">Você também pode [criar NSGs no modelo de implantação clássica](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="398fd-105">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="398fd-106">O exemplo de comando PowerShell abaixo espera um ambiente simples já criado com base no cenário acima.</span><span class="sxs-lookup"><span data-stu-id="398fd-106">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="398fd-107">Se você quiser executar os comandos conforme eles são exibidos neste documento, primeiro crie o ambiente de teste ao implantar [esse modelo](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), clique em **Implantar no Azure**, substitua os valores de parâmetro padrão, se necessário, e siga as instruções no portal.</span><span class="sxs-lookup"><span data-stu-id="398fd-107">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span> <span data-ttu-id="398fd-108">As etapas abaixo usam **RG-NSG** como o nome do grupo de recursos no qual o modelo foi implantado.</span><span class="sxs-lookup"><span data-stu-id="398fd-108">The steps below use **RG-NSG** as the name of the resource group the template was deployed to.</span></span>

## <a name="create-the-nsg-frontend-nsg"></a><span data-ttu-id="398fd-109">Criar o NSG NSG-FrontEnd</span><span class="sxs-lookup"><span data-stu-id="398fd-109">Create the NSG-FrontEnd NSG</span></span>
<span data-ttu-id="398fd-110">Para criar o NSG **NSG-FrontEnd** , como mostra o cenário acima, siga as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="398fd-110">To create the **NSG-FrontEnd** NSG as shown in the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="398fd-111">Em um navegador, navegue até http://portal.azure.com e, se necessário, entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="398fd-111">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="398fd-112">Clique em **Procurar >** > **Grupos de segurança de rede**.</span><span class="sxs-lookup"><span data-stu-id="398fd-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Portal do Azure - NSGs](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="398fd-114">Na folha **Grupos de segurança de rede**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="398fd-114">In the **Network security groups** blade, click **Add**.</span></span>
   
    ![Portal do Azure - NSGs](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="398fd-116">Na folha **Criar grupo de segurança de rede**, crie um NSG chamado *NSG-FrontEnd* no grupo de recursos *RG-NSG* e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="398fd-116">In the **Create network security group** blade, create an NSG named *NSG-FrontEnd* in the *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Portal do Azure - NSGs](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="398fd-118">Criar regras em um NSG existente</span><span class="sxs-lookup"><span data-stu-id="398fd-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="398fd-119">Para criar regras em um NSG existente por meio do portal do Azure, siga as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="398fd-119">To create rules in an existing NSG from the Azure portal, follow the steps below.</span></span>

1. <span data-ttu-id="398fd-120">Clique em **Procurar >** > **Grupos de segurança de rede**.</span><span class="sxs-lookup"><span data-stu-id="398fd-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="398fd-121">Na lista de NSGs, clique em **NSG-FrontEnd** > **Regras de segurança de entrada**</span><span class="sxs-lookup"><span data-stu-id="398fd-121">In the list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Portal do Azure - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="398fd-123">Na lista de **Regras de segurança de entrada**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="398fd-123">In the list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Portal do Azure - Adicionar regra](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="398fd-125">Na folha **Adicionar regra de segurança de entrada**, crie uma regra chamada *web-rule* com prioridade de *200* permitindo o acesso via *TCP* à porta *80* a qualquer VM por meio de qualquer origem e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="398fd-125">In the **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* to port *80* to any VM from any source, and then click **OK**.</span></span> <span data-ttu-id="398fd-126">Observe como a maioria destas configurações já é o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="398fd-126">Notice that most of these settings are default values already.</span></span>
   
    ![Portal do Azure - Configurações de regra](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="398fd-128">Depois de alguns segundos, você encontrará a nova regra no NSG.</span><span class="sxs-lookup"><span data-stu-id="398fd-128">After a few seconds you will see the new rule in the NSG.</span></span>
   
    ![Portal do Azure - Nova regra](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="398fd-130">Repita as etapas até 6 para criar uma regra de entrada chamada *rdp-rule* com uma prioridade de *250* permitindo o acesso via *TCP* à porta *3389* a qualquer VM de qualquer origem.</span><span class="sxs-lookup"><span data-stu-id="398fd-130">Repeat steps  to 6 to create an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* to port *3389* to any VM from any source.</span></span>

## <a name="associate-the-nsg-to-the-frontend-subnet"></a><span data-ttu-id="398fd-131">Associar o NSG à sub-rede FrontEnd</span><span class="sxs-lookup"><span data-stu-id="398fd-131">Associate the NSG to the FrontEnd subnet</span></span>
1. <span data-ttu-id="398fd-132">Clique em **Procurar >** > **Grupos de recursos** > **RG-NSG**.</span><span class="sxs-lookup"><span data-stu-id="398fd-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="398fd-133">Na folha**RG-NSG**, clique em **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="398fd-133">In the **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Portal do Azure - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="398fd-135">Na folha **Configurações**, clique em **Sub-redes** > **FrontEnd** > **Grupo de segurança de rede** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="398fd-135">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Portal do Azure - Configurações de sub-rede](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="398fd-137">Na folha **FrontEnd**, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="398fd-137">In the **FrontEnd** blade, click **Save**.</span></span>
   
    ![Portal do Azure - Configurações de sub-rede](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-the-nsg-backend-nsg"></a><span data-ttu-id="398fd-139">Criar o NSG NSG-BackEnd</span><span class="sxs-lookup"><span data-stu-id="398fd-139">Create the NSG-BackEnd NSG</span></span>
<span data-ttu-id="398fd-140">Para criar o NSG **NSG-BackEnd** e associá-lo à sub-rede **BackEnd**, siga as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="398fd-140">To create the **NSG-BackEnd** NSG and associate it to the **BackEnd** subnet, follow the steps below.</span></span>

1. <span data-ttu-id="398fd-141">Repita as etapas descritas em [Criar o NSG NSG-FrontEnd](#Create-the-NSG-FrontEnd-NSG) para criar um NSG chamado *NSG-BackEnd*</span><span class="sxs-lookup"><span data-stu-id="398fd-141">Repeat the steps in [Create the NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) to create an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="398fd-142">Repita as etapas descritas em [Criar regras em um NSG existente](#Create-rules-in-an-existing-NSG) para criar as regras de **entrada** na tabela abaixo.</span><span class="sxs-lookup"><span data-stu-id="398fd-142">Repeat the steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) to create the **inbound** rules in the table below.</span></span>
   
   | <span data-ttu-id="398fd-143">Regra de entrada</span><span class="sxs-lookup"><span data-stu-id="398fd-143">Inbound rule</span></span> | <span data-ttu-id="398fd-144">Regra de saída</span><span class="sxs-lookup"><span data-stu-id="398fd-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Portal do Azure - regra de entrada](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Portal do Azure - regra de saída](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="398fd-147">Repita as etapas descritas em [Associar o NSG à sub-rede FrontEnd](#Associate-the-NSG-to-the-FrontEnd-subnet) para associar o NSG **NSG-Backend** à sub-rede **BackEnd**.</span><span class="sxs-lookup"><span data-stu-id="398fd-147">Repeat the steps in [Associate the NSG to the FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) to associate the **NSG-Backend** NSG to the **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="398fd-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="398fd-148">Next Steps</span></span>
* <span data-ttu-id="398fd-149">Saiba como [gerenciar NSGs existentes](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="398fd-149">Learn how to [manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="398fd-150">[Habilite o registro em log](virtual-network-nsg-manage-log.md) para NSGs.</span><span class="sxs-lookup"><span data-stu-id="398fd-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

