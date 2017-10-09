---
title: "endereços IP privados de aaaConfigure para VMs - portal do Azure | Microsoft Docs"
description: "Saiba como tooconfigure endereços IP para máquinas virtuais usando Olá portal do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="f1323-103">Configurar endereços IP para uma máquina virtual usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f1323-103">Configure private IP addresses for a virtual machine using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1323-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f1323-104">Azure portal</span></span>](virtual-networks-static-private-ip-arm-pportal.md)
> * [<span data-ttu-id="f1323-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1323-105">PowerShell</span></span>](virtual-networks-static-private-ip-arm-ps.md)
> * [<span data-ttu-id="f1323-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f1323-106">Azure CLI</span></span>](virtual-networks-static-private-ip-arm-cli.md)
> * [<span data-ttu-id="f1323-107">Portal do Azure (Clássico)</span><span class="sxs-lookup"><span data-stu-id="f1323-107">Azure portal (Classic)</span></span>](virtual-networks-static-private-ip-classic-pportal.md)
> * [<span data-ttu-id="f1323-108">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="f1323-108">PowerShell (Classic)</span></span>](virtual-networks-static-private-ip-classic-ps.md)
> * [<span data-ttu-id="f1323-109">CLI do Azure (Clássica)</span><span class="sxs-lookup"><span data-stu-id="f1323-109">Azure CLI (Classic)</span></span>](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="f1323-110">Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1323-110">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="f1323-111">Você também pode [gerenciar o endereço IP privado estático no modelo de implantação clássico Olá](virtual-networks-static-private-ip-classic-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="f1323-111">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-pportal.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="f1323-112">etapas do exemplo Hello abaixo esperam um ambiente simples já criado.</span><span class="sxs-lookup"><span data-stu-id="f1323-112">hello sample steps below expect a simple environment already created.</span></span> <span data-ttu-id="f1323-113">Se você quiser etapas de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste de hello, descrito em [criar uma rede virtual](virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="f1323-113">If you want toorun hello steps as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-pportal.md).</span></span>

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a><span data-ttu-id="f1323-114">Como toocreate uma máquina virtual para teste de IP privado estático endereços</span><span class="sxs-lookup"><span data-stu-id="f1323-114">How toocreate a VM for testing static private IP addresses</span></span>
<span data-ttu-id="f1323-115">Você não pode definir um endereço IP privado estático durante a criação de saudação de uma VM no modo de implantação do Gerenciador de recursos de saudação usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1323-115">You cannot set a static private IP address during hello creation of a VM in hello Resource Manager deployment mode by using hello Azure portal.</span></span> <span data-ttu-id="f1323-116">Primeiro você deve criar hello VM, tehn defina sua toobe IP privado estático.</span><span class="sxs-lookup"><span data-stu-id="f1323-116">You must create hello VM first, tehn set its private IP toobe static.</span></span>

<span data-ttu-id="f1323-117">toocreate uma VM denominada *DNS01* em Olá *front-end* sub-rede de uma rede virtual denominada *TestVNet*, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="f1323-117">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet*, follow hello steps below.</span></span>

1. <span data-ttu-id="f1323-118">Em um navegador, navegue toohttp://portal.azure.com e, se necessário, entre com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1323-118">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="f1323-119">Clique em **novo** > **de computação** > **Windows Server 2012 R2 Datacenter**, observe que Olá **selecionar um modelo de implantação** já lista mostra **Gerenciador de recursos de**e, em seguida, clique em **criar**, como mostrado na figura de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="f1323-119">Click **NEW** > **Compute** > **Windows Server 2012 R2 Datacenter**, notice that hello **Select a deployment model** list already shows **Resource Manager**, and then click **Create**, as seen in hello figure below.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. <span data-ttu-id="f1323-121">Em Olá **Noções básicas de** folha, digite nome de saudação do hello VM toobe criado (*DNS01* em nosso cenário), Olá a conta de administrador local e senha, como mostrado na figura abaixo a saudação.</span><span class="sxs-lookup"><span data-stu-id="f1323-121">In hello **Basics** blade, enter hello name of hello VM toobe created (*DNS01* in our scenario), hello local administrator account, and password, as seen in hello figure below.</span></span>
   
    ![Folha de Noções básicas](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. <span data-ttu-id="f1323-123">Tornar-se de saudação **local** selecionado é *centro dos EUA*, em seguida, clique em **selecionar existentes** em **grupo de recursos**, clique **Grupo de recursos** novamente, em seguida, clique em *TestRG*e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="f1323-123">Make sure hello **Location** selected is *Central US*, then click **Select existing** under **Resource group**, then click **Resource group** again, then click *TestRG*, and then click **OK**.</span></span>
   
    ![Folha de Noções básicas](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. <span data-ttu-id="f1323-125">Em Olá **escolher um tamanho de** folha, selecione **A1 padrão**e, em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="f1323-125">In hello **Choose a size** blade, select **A1 Standard**, and then click **Select**.</span></span>
   
    ![Escolha uma folha de tamanho](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. <span data-ttu-id="f1323-127">No **configurações** folha, verifique Olá se seguintes propriedades são definidas são definidas com valores de saudação abaixo e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="f1323-127">In teh **Settings** blade, make sure hello following properties are set are set with hello values below, and then click **OK**.</span></span>
   
    <span data-ttu-id="f1323-128">-**Conta de armazenamento**: *vnetstorage*</span><span class="sxs-lookup"><span data-stu-id="f1323-128">-**Storage account**: *vnetstorage*</span></span>
   
   * <span data-ttu-id="f1323-129">**Rede**: *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="f1323-129">**Network**: *TestVNet*</span></span>
   * <span data-ttu-id="f1323-130">**Sub-rede**: *FrontEnd*</span><span class="sxs-lookup"><span data-stu-id="f1323-130">**Subnet**: *FrontEnd*</span></span>
     
     ![Escolha uma folha de tamanho](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. <span data-ttu-id="f1323-132">Em Olá **resumo** folha, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="f1323-132">In hello **Summary** blade, click **OK**.</span></span> <span data-ttu-id="f1323-133">Aviso Olá bloco abaixo exibido no painel.</span><span class="sxs-lookup"><span data-stu-id="f1323-133">Notice hello tile below displayed in your dashboard.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="f1323-135">Como informações de uma VM de endereço de IP privado estático de tooretrieve</span><span class="sxs-lookup"><span data-stu-id="f1323-135">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="f1323-136">tooview Olá privadas informações endereços IP estáticos para Olá VM criada com etapas de saudação acima, execute as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="f1323-136">tooview hello static private IP address information for hello VM created with hello steps above, execute hello steps below.</span></span>

1. <span data-ttu-id="f1323-137">No portal do Azure Azure hello, clique em **procurar todos os** > **máquinas virtuais** > **DNS01** > **todos configurações de** > **interfaces de rede** e, em seguida, clique na interface de rede somente Olá listado.</span><span class="sxs-lookup"><span data-stu-id="f1323-137">From hello Azure Azure portal, click **BROWSE ALL** > **Virtual machines** > **DNS01** > **All settings** > **Network interfaces** and then click on hello only network interface listed.</span></span>
   
    ![Implantando o bloco VM](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. <span data-ttu-id="f1323-139">Em Olá **interface de rede** folha, clique em **todas as configurações** > **endereços IP** e observe hello **atribuição** e **Endereço IP** valores.</span><span class="sxs-lookup"><span data-stu-id="f1323-139">In hello **Network interface** blade, click **All settings** > **IP addresses** and notice hello **Assignment** and **IP address** values.</span></span>
   
    ![Implantando o bloco VM](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="f1323-141">Como tooadd um endereço IP privado estático endereço tooan existente VM</span><span class="sxs-lookup"><span data-stu-id="f1323-141">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="f1323-142">tooadd um toohello de endereço IP de privado estático VM criada usando Olá etapas acima, siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="f1323-142">tooadd a static private IP address toohello VM created using hello steps above, follow hello steps below:</span></span>

1. <span data-ttu-id="f1323-143">De saudação **endereços IP** folha mostrada acima, clique em **estático** em **atribuição**.</span><span class="sxs-lookup"><span data-stu-id="f1323-143">From hello **IP addresses** blade shown above, click **Static** under **Assignment**.</span></span>
2. <span data-ttu-id="f1323-144">Digite *192.168.1.101* para **Endereço IP**, e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f1323-144">Type *192.168.1.101* for **IP address**, and then click **Save**.</span></span>
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> <span data-ttu-id="f1323-146">Se, depois de clicar em **salvar** você notar que a atribuição Olá ainda está definida muito**dinâmico**, isso significa que o endereço IP hello digitado já está em uso.</span><span class="sxs-lookup"><span data-stu-id="f1323-146">If after clicking **Save** you notice that hello assignment is still set too**Dynamic**, it means that hello IP address you typed is already in use.</span></span> <span data-ttu-id="f1323-147">Tente um endereço IP diferente.</span><span class="sxs-lookup"><span data-stu-id="f1323-147">Try a different IP address.</span></span>
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="f1323-148">Como tooremove um particular de endereços IP estáticos de uma VM</span><span class="sxs-lookup"><span data-stu-id="f1323-148">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="f1323-149">tooremove Olá endereço IP privado estático de saudação VM criada acima, conclua Olá etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1323-149">tooremove hello static private IP address from hello VM created above, complete hello following step:</span></span>

<span data-ttu-id="f1323-150">De saudação **endereços IP** folha mostrada acima, clique em **dinâmico** em **atribuição**e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="f1323-150">From hello **IP addresses** blade shown above, click **Dynamic** under **Assignment**, and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1323-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f1323-151">Next steps</span></span>
* <span data-ttu-id="f1323-152">Saiba mais sobre endereços [IP públicos reservados](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="f1323-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="f1323-153">Saiba mais sobre endereços [ILPIP (IP público em nível de instância)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="f1323-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="f1323-154">Consulte Olá [APIs de REST de IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1323-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

