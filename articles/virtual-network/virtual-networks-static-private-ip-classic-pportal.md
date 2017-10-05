---
title: "Configurar endereços IP para máquinas virtuais (Clássicas) - Portal do Azure | Microsoft Docs"
description: "Saiba como configurar endereços IP para máquinas virtuais (Clássico) usando o Portal do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bde6de3495c2909b63b1f85e420a4ff5e7ac2c1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-the-azure-portal"></a><span data-ttu-id="b4032-103">Configurar endereços IP particulares para uma máquina virtual (Clássica) usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b4032-103">Configure private IP addresses for a virtual machine (Classic) using the Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="b4032-104">Este artigo aborda o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="b4032-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="b4032-105">Você também pode [gerenciar um endereço IP privado estático no modelo de implantação do Gerenciador de Recursos](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="b4032-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="b4032-106">As etapas de exemplo abaixo esperam um ambiente simples já criado.</span><span class="sxs-lookup"><span data-stu-id="b4032-106">The sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="b4032-107">Se você quiser executar as etapas da forma como elas aparecem neste documento, primeiro crie o ambiente de teste descrito em [criar uma vnet](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="b4032-107">If you want to run the steps as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-to-specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="b4032-108">Como especificar um endereço IP privado estático ao criar uma VM</span><span class="sxs-lookup"><span data-stu-id="b4032-108">How to specify a static private IP address when creating a VM</span></span>
<span data-ttu-id="b4032-109">Para criar uma VM denominada *DNS01* na sub-rede *FrontEnd* de uma VNet chamada *TestVNet* com o endereço IP privado estático *192.168.1.101*, execute as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="b4032-109">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="b4032-110">Em um navegador, navegue até http://portal.azure.com e, se necessário, entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4032-110">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="b4032-111">Clique em **NOVO** > **Computação** > **Windows Server 2012 R2 Datacenter**, observe que a lista **Selecionar um modelo de implantação** já mostra **Clássico** e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b4032-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that the **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="b4032-113">Na folha **Criar VM** , insira o nome da VM a ser criada (*DNS01* em nosso cenário), a conta de administrador local e a senha.</span><span class="sxs-lookup"><span data-stu-id="b4032-113">In the **Create VM** blade, enter the name of the VM to be created (*DNS01* in our scenario), the local administrator account, and password.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="b4032-115">Clique em **Configuração opcional** > **Rede** > **Rede Virtual**, e, em seguida, clique em **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="b4032-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="b4032-116">Se **TestVNet** não estiver disponível, verifique se você está usando o *Centro dos EUA* como local e que você criou o ambiente de teste descrito no início deste artigo.</span><span class="sxs-lookup"><span data-stu-id="b4032-116">If **TestVNet** is not available, make sure you are using the *Central US* location and have created the test environment described at the beginning of this article.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="b4032-118">Na folha **Rede**, certifique-se de que a sub-rede selecionada atualmente é *FrontEnd*, em seguida, clique em **Endereços IP**, em **Atribuição de endereço IP** clique em **Estático**, e, em seguida, digite *192.168.1.101* para **Endereço IP** conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="b4032-118">In the **Network** blade, make sure the subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="b4032-120">Clique em **OK** na folha **Endereços IP**, em seguida, clique em **OK** na folha **Rede** e clique em **OK** na folha **Configuração opcional**.</span><span class="sxs-lookup"><span data-stu-id="b4032-120">Click **OK** in the **IP addresses** blade, then click **OK** in the **Network** blade, and click **OK** in the **Optional config** blade.</span></span>
7. <span data-ttu-id="b4032-121">Na folha **Criar VM**, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b4032-121">In the **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="b4032-122">Observe o bloco abaixo exibido no painel.</span><span class="sxs-lookup"><span data-stu-id="b4032-122">Notice the tile below displayed in your dashboard.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="b4032-124">Como recuperar informações do endereço IP privado estático de uma VM</span><span class="sxs-lookup"><span data-stu-id="b4032-124">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="b4032-125">Para exibir as informações de endereço IP privado estático para a VM criada com as etapas acima, execute as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="b4032-125">To view the static private IP address information for the VM created with the steps above, execute the steps below.</span></span>

1. <span data-ttu-id="b4032-126">No portal do Azure, clique em **PROCURAR TUDO** > **Máquinas virtuais (clássico)** > **DNS01** > **Todas as configurações** > **Endereços IP** e observe o endereço IP e a atribuição de endereço IP, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="b4032-126">From the Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice the IP address assignment and IP address as seen below.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="b4032-128">Como remover o endereço IP privado estático de uma VM</span><span class="sxs-lookup"><span data-stu-id="b4032-128">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="b4032-129">Para remover o endereço IP privado estático da VM criada acima, siga as etapas abaixo.</span><span class="sxs-lookup"><span data-stu-id="b4032-129">To remove the static private IP address from the VM created above, follow the steps below.</span></span>

1. <span data-ttu-id="b4032-130">Na folha **Endereços IP** mostrada acima, clique em **Dinâmico** à direita da **Atribuição de endereço IP**, em seguida, clique em **Salvar**, e, em seguida, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="b4032-130">From the **IP addresses** blade shown above, click **Dynamic** to the right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="b4032-132">Como adicionar um endereço IP privado estático a uma VM existente</span><span class="sxs-lookup"><span data-stu-id="b4032-132">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="b4032-133">Para adicionar um IP privado estático à VM criada usando as etapas acima, execute as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="b4032-133">To add a static private IP address to the VM created using the steps above, follow the steps below:</span></span>

1. <span data-ttu-id="b4032-134">Na folha **Endereços IP** mostrada acima, clique em **Estático** à direita de **Atribuição de endereço IP**.</span><span class="sxs-lookup"><span data-stu-id="b4032-134">From the **IP addresses** blade shown above, click **Static** to the right of **IP address assignment**.</span></span>
2. <span data-ttu-id="b4032-135">Digite *192.168.1.101* para **Endereço IP**, clique em **Salvar** e, em seguida, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="b4032-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4032-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b4032-136">Next steps</span></span>
* <span data-ttu-id="b4032-137">Saiba mais sobre endereços [IP públicos reservados](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="b4032-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="b4032-138">Saiba mais sobre endereços [ILPIP (IP público em nível de instância)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="b4032-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="b4032-139">Consulte as [APIs REST de IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4032-139">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

