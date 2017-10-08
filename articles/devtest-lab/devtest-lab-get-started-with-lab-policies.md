---
title: "políticas de laboratório básico aaaManage no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como tooset algumas das políticas básica de saudação (configurações) para um laboratório DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="ca10e-103">Gerenciar políticas básicas para um laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ca10e-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="ca10e-104">Azure DevTest Labs permite toocontrol custo e minimizar os desperdícios em seus laboratórios Gerenciando políticas (configurações) para cada laboratório.</span><span class="sxs-lookup"><span data-stu-id="ca10e-104">Azure DevTest Labs enables you toocontrol cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="ca10e-105">Neste artigo, você Introdução às políticas aprendendo como tooset duas políticas mais críticas do hello - limitando Olá número de máquinas virtuais (VM) que pode ser criadas ou solicitadas por um único usuário e desligamento automáticos configuração.</span><span class="sxs-lookup"><span data-stu-id="ca10e-105">In this article, you get started with policies by learning how tooset two of hello most critical policies - limiting hello number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="ca10e-106">tooview como tooset cada política de laboratório, consulte o artigo hello, [definir políticas de laboratório no Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ca10e-106">tooview how tooset every lab policy, see hello article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="ca10e-107">Acessar as políticas de laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ca10e-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="ca10e-108">Olá etapas a seguir orientam você durante a configuração de políticas para um laboratório no Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="ca10e-108">hello following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="ca10e-109">as políticas de Olá tooview (e alterar) para um ambiente de laboratório, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ca10e-109">tooview (and change) hello policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="ca10e-110">Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="ca10e-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="ca10e-111">Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca10e-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="ca10e-112">Saudação de laboratórios, selecione lista laboratório desejado hello.</span><span class="sxs-lookup"><span data-stu-id="ca10e-112">From hello list of labs, select hello desired lab.</span></span>   

1. <span data-ttu-id="ca10e-113">Selecione **Configuração e políticas**.</span><span class="sxs-lookup"><span data-stu-id="ca10e-113">Select **Configuration and policies**.</span></span>

    ![Folha de configurações de política](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="ca10e-115">Olá **políticas e configurações** folha contém um menu de configurações que você pode especificar.</span><span class="sxs-lookup"><span data-stu-id="ca10e-115">hello **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="ca10e-116">Este artigo aborda apenas as configurações de saudação de **máquinas virtuais por usuário** e **desligamento automático**.</span><span class="sxs-lookup"><span data-stu-id="ca10e-116">This article covers only hello settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="ca10e-117">toolearn sobre Olá restantes configurações, consulte [gerenciar todas as políticas para um laboratório no Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="ca10e-117">toolearn about hello remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="ca10e-118">Conjunto de máquinas virtuais por usuário</span><span class="sxs-lookup"><span data-stu-id="ca10e-118">Set virtual machines per user</span></span>
<span data-ttu-id="ca10e-119">Olá política para **máquinas virtuais por usuário** permite a você toospecify Olá alto número de máquinas virtuais que podem ser criados por um usuário individual.</span><span class="sxs-lookup"><span data-stu-id="ca10e-119">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="ca10e-120">Se um usuário tentar toocreate ou declaração de uma máquina virtual quando o limite de saudação do usuário foram atendido, uma mensagem de erro indica que Olá que VM não pode ser criado/exigida.</span><span class="sxs-lookup"><span data-stu-id="ca10e-120">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="ca10e-121">No laboratório de saudação **políticas e configurações** menu, selecione **máquinas virtuais por usuário**.</span><span class="sxs-lookup"><span data-stu-id="ca10e-121">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Máquinas virtuais por usuário](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="ca10e-123">Selecione **Sim** toolimit Olá diversas VMs por usuário.</span><span class="sxs-lookup"><span data-stu-id="ca10e-123">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="ca10e-124">Se você não quiser toolimit Olá diversas VMs por usuário, selecione **não**.</span><span class="sxs-lookup"><span data-stu-id="ca10e-124">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="ca10e-125">Se você selecionar **Sim**, insira um valor numérico que indica o número máximo de saudação de VMs que pode ser criado ou solicitado por um usuário.</span><span class="sxs-lookup"><span data-stu-id="ca10e-125">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="ca10e-126">Selecione **Sim** toolimit diversas Olá VMs que pode usar SSD (disco de estado sólido).</span><span class="sxs-lookup"><span data-stu-id="ca10e-126">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="ca10e-127">Se você não quiser toolimit diversas Olá VMs que pode usar o SSD, selecione **não**.</span><span class="sxs-lookup"><span data-stu-id="ca10e-127">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="ca10e-128">Se você selecionar **Sim**, insira um valor que indica o número máximo de saudação de máquinas virtuais que podem ser criados usando SSD.</span><span class="sxs-lookup"><span data-stu-id="ca10e-128">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="ca10e-129">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ca10e-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="ca10e-130">Definir desligamento automático</span><span class="sxs-lookup"><span data-stu-id="ca10e-130">Set auto-shutdown</span></span>
<span data-ttu-id="ca10e-131">política de desligamento automático de saudação ajuda toominimize laboratório desperdiçar, permitindo que você tenha tempo de saudação toospecify que VMs deste laboratório desligadas.</span><span class="sxs-lookup"><span data-stu-id="ca10e-131">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="ca10e-132">No laboratório de saudação **políticas e configurações** folha, selecione **desligamento automático**.</span><span class="sxs-lookup"><span data-stu-id="ca10e-132">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Desligamento automático](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="ca10e-134">Selecione **na** tooenable essa política, e **Off** toodisable-lo.</span><span class="sxs-lookup"><span data-stu-id="ca10e-134">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="ca10e-135">Se você habilitar essa política, especifique Olá tooshut de tempo (e o fuso horário) para todas as máquinas virtuais no laboratório atual hello.</span><span class="sxs-lookup"><span data-stu-id="ca10e-135">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="ca10e-136">Especifique **Sim** ou **não** para Olá opção toosend uma toohello anterior de 15 minutos de notificação especificado o tempo de desligamento automático.</span><span class="sxs-lookup"><span data-stu-id="ca10e-136">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="ca10e-137">Se você especificar **Sim**, insira uma notificação de saudação tooreceive de ponto de extremidade do webhook URL.</span><span class="sxs-lookup"><span data-stu-id="ca10e-137">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="ca10e-138">Para saber mais sobre os webhooks, veja [Criar um webhook ou uma função da API do Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="ca10e-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="ca10e-139">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ca10e-139">Select **Save**.</span></span>

    <span data-ttu-id="ca10e-140">Por padrão, uma vez habilitada, essa diretiva se aplica a tooall VMs no laboratório atual hello.</span><span class="sxs-lookup"><span data-stu-id="ca10e-140">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="ca10e-141">tooremove essa configuração de uma VM específica, abra da VM Olá folha e altere seu **desligamento automático** configuração</span><span class="sxs-lookup"><span data-stu-id="ca10e-141">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="ca10e-142">Definir início automático</span><span class="sxs-lookup"><span data-stu-id="ca10e-142">Set auto-start</span></span>
<span data-ttu-id="ca10e-143">política de início automático Olá permite toospecify quando Olá máquinas virtuais no laboratório atual Olá deve ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="ca10e-143">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="ca10e-144">No laboratório de saudação **políticas e configurações** folha, selecione **Auto-start**.</span><span class="sxs-lookup"><span data-stu-id="ca10e-144">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Início automático](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="ca10e-146">Selecione **na** tooenable essa política, e **Off** toodisable-lo.</span><span class="sxs-lookup"><span data-stu-id="ca10e-146">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="ca10e-147">Se você habilitar essa política, especifique a hora de início agendada de saudação, fuso horário e Olá dias da semana Olá para qual Olá tempo se aplica.</span><span class="sxs-lookup"><span data-stu-id="ca10e-147">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="ca10e-148">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ca10e-148">Select **Save**.</span></span>

    <span data-ttu-id="ca10e-149">Uma vez habilitada, essa política não é aplicada automaticamente tooany VMs no laboratório atual Olá.</span><span class="sxs-lookup"><span data-stu-id="ca10e-149">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="ca10e-150">tooapply tooa essa configuração VM específica, folha e alteração da VM Olá abrir seu **Auto-start** configuração</span><span class="sxs-lookup"><span data-stu-id="ca10e-150">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ca10e-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ca10e-151">Next steps</span></span>

- <span data-ttu-id="ca10e-152">[Definir políticas de laboratório no Azure DevTest Labs](devtest-lab-set-lab-policy.md) -Saiba como toomodify outras políticas de laboratório</span><span class="sxs-lookup"><span data-stu-id="ca10e-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how toomodify other lab policies</span></span> 
