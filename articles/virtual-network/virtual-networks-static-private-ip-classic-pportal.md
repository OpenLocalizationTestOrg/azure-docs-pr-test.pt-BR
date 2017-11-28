---
title: "endereços IP privados de aaaConfigure para VMs (clássico) - portal do Azure | Microsoft Docs"
description: "Saiba como tooconfigure endereços IP para máquinas virtuais (clássico) usando Olá portal do Azure."
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
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a><span data-ttu-id="afbb8-103">Configurar endereços IP para uma máquina virtual (clássica) usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="afbb8-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="afbb8-104">Este artigo aborda o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="afbb8-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="afbb8-105">Você também pode [gerenciar um endereço IP privado estático no modelo de implantação do Gerenciador de recursos de saudação](virtual-networks-static-private-ip-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="afbb8-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="afbb8-106">etapas do exemplo Hello abaixo esperam um ambiente simples já criado.</span><span class="sxs-lookup"><span data-stu-id="afbb8-106">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="afbb8-107">Se você quiser etapas de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste de hello, descrito em [criar uma rede virtual](virtual-networks-create-vnet-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="afbb8-107">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-pportal.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="afbb8-108">Como toospecify um particular de endereços IP estáticos ao criar uma VM</span><span class="sxs-lookup"><span data-stu-id="afbb8-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="afbb8-109">toocreate uma VM denominada *DNS01* em Olá *front-end* sub-rede de uma rede virtual denominada *TestVNet* com um endereço IP privado estático de *192.168.1.101*, Siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="afbb8-109">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="afbb8-110">Em um navegador, navegue toohttp://portal.azure.com e, se necessário, entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="afbb8-110">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="afbb8-111">Clique em **novo** > **de computação** > **Windows Server 2012 R2 Datacenter**, observe que Olá **selecionar um modelo de implantação** já lista mostra **clássico**e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="afbb8-111">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Classic**, and then click **Create**.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. <span data-ttu-id="afbb8-113">Em Olá **criar VM** folha, digite nome de saudação do hello VM toobe criado (*DNS01* em nosso cenário), Olá a conta de administrador local e a senha.</span><span class="sxs-lookup"><span data-stu-id="afbb8-113">In hello **Create VM** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. <span data-ttu-id="afbb8-115">Clique em **Configuração opcional** > **Rede** > **Rede Virtual**, e, em seguida, clique em **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="afbb8-115">Click **Optional Configuration** > **Network** > **Virtual Network**, and then click **TestVNet**.</span></span> <span data-ttu-id="afbb8-116">Se **TestVNet** não estiver disponível, verifique se você está usando Olá *centro dos EUA* local e criou o ambiente de teste Olá descrita no início deste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="afbb8-116">If **TestVNet** is not available, make sure you are using hello *Central US* location and have created hello test environment described at hello beginning of this article.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. <span data-ttu-id="afbb8-118">Em Olá **rede** folha, verifique se Olá a sub-rede selecionada no momento é *front-end*, em seguida, clique em **endereços IP**, em **aatribuiçãodeendereçoIP** clique **estático**e, em seguida, digite *192.168.1.101* para **endereço IP** conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="afbb8-118">In hello **Network** blade, make sure hello subnet currently selected is *FrontEnd*, then click **IP addresses**, under **IP address assignment** click **Static**, and then enter *192.168.1.101* for **IP Address** as seen below.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. <span data-ttu-id="afbb8-120">Clique em **Okey** em Olá **endereços IP** folha, em seguida, clique em **Okey** em Olá **rede** folha e clique em **Okey**em Olá **configuração opcional** folha.</span><span class="sxs-lookup"><span data-stu-id="afbb8-120">Click **OK** in hello **IP addresses** blade, then click **OK** in hello **Network** blade, and click **OK** in hello **Optional config** blade.</span></span>
7. <span data-ttu-id="afbb8-121">Em Olá **criar VM** folha, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="afbb8-121">In hello **Create VM** blade, click **Create**.</span></span> <span data-ttu-id="afbb8-122">Aviso Olá bloco abaixo exibido no painel.</span><span class="sxs-lookup"><span data-stu-id="afbb8-122">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="afbb8-124">Como informações de uma VM de endereço de IP privado estático de tooretrieve</span><span class="sxs-lookup"><span data-stu-id="afbb8-124">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="afbb8-125">tooview Olá privadas informações endereços IP estáticos para Olá VM criada com etapas de saudação acima, execute as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="afbb8-125">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="afbb8-126">No portal do Azure Azure hello, clique em **procurar todos os** > **máquinas virtuais (clássicas)** > **DNS01**  >   **Todas as configurações** > **endereços IP** e observe Olá a atribuição de endereço IP e endereço IP, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="afbb8-126">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines (classic)** > **DNS01** > **All settings** > **IP addresses** and notice hello IP address assignment and IP address as seen below.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="afbb8-128">Como tooremove um particular de endereços IP estáticos de uma VM</span><span class="sxs-lookup"><span data-stu-id="afbb8-128">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="afbb8-129">tooremove Olá endereço IP privado estático de saudação VM criada anteriormente, execute as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="afbb8-129">tooremove hello static private IP address from hello VM created above, follow hello steps below.</span></span>

1. <span data-ttu-id="afbb8-130">De saudação **endereços IP** folha mostrada acima, clique em **dinâmico** toohello à direita do **atribuição de endereço IP**, em seguida, clique em **salvar**e, em seguida, Clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="afbb8-130">From hello **IP addresses** blade shown above, click **Dynamic** toohello right of **IP address assignment**, then click **Save**, and then click **Yes**.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="afbb8-132">Como tooadd um endereço IP privado estático endereço tooan existente VM</span><span class="sxs-lookup"><span data-stu-id="afbb8-132">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="afbb8-133">tooadd um toohello de endereço IP de privado estático VM criada usando Olá etapas acima, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="afbb8-133">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="afbb8-134">De saudação **endereços IP** folha mostrada acima, clique em **estático** toohello à direita do **atribuição de endereço IP**.</span><span class="sxs-lookup"><span data-stu-id="afbb8-134">From hello **IP addresses** blade shown above, click **Static** toohello right of **IP address assignment**.</span></span>
2. <span data-ttu-id="afbb8-135">Digite *192.168.1.101* para **Endereço IP**, clique em **Salvar** e, em seguida, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="afbb8-135">Type *192.168.1.101* for **IP address**, then click **Save**, and then click **Yes**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afbb8-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="afbb8-136">Next steps</span></span>
* <span data-ttu-id="afbb8-137">Saiba mais sobre endereços [IP públicos reservados](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="afbb8-137">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="afbb8-138">Saiba mais sobre endereços [ILPIP (IP público em nível de instância)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="afbb8-138">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="afbb8-139">Consulte Olá [APIs de REST de IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="afbb8-139">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

