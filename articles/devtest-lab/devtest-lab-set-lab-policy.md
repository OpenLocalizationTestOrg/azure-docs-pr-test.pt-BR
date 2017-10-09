---
title: "políticas de laboratório aaaManage no Azure DevTest Labs | Microsoft Docs"
description: "Saiba como os tamanhos de políticas de laboratório toodefine como VMs, VMs máximo por usuário e a automação de desligamento."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="7e900-103">Gerenciar todas as políticas de um laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="7e900-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="7e900-104">O Azure DevTest Labs permite controlar o custo e minimize o desperdício nos laboratórios gerenciando políticas (configurações) de cada laboratório.</span><span class="sxs-lookup"><span data-stu-id="7e900-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="7e900-105">Este artigo explica detalhadamente como tooset cada política.</span><span class="sxs-lookup"><span data-stu-id="7e900-105">This article explains in step-by-step detail how tooset each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="7e900-106">Definir tamanhos de máquina virtual permitidos</span><span class="sxs-lookup"><span data-stu-id="7e900-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="7e900-107">Hello política para Olá configuração permitidos tamanhos de VM ajuda toominimize laboratório desperdiçar, permitindo que você toospecify quais tamanhos de VM são permitidos em laboratório hello.</span><span class="sxs-lookup"><span data-stu-id="7e900-107">hello policy for setting hello allowed VM sizes helps toominimize lab waste by enabling you toospecify which VM sizes are allowed in hello lab.</span></span> <span data-ttu-id="7e900-108">Se essa política está ativada, apenas os tamanhos de VM da lista podem ser usado toocreate VMs.</span><span class="sxs-lookup"><span data-stu-id="7e900-108">If this policy is activated, only VM sizes from this list can be used toocreate VMs.</span></span>

1. <span data-ttu-id="7e900-109">No laboratório de saudação **políticas e configurações** folha, selecione **permitidos tamanhos de máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="7e900-109">On hello lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![Tamanhos de máquinas virtuais permitidos](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="7e900-111">Selecione **na** tooenable essa política, e **Off** toodisable-lo.</span><span class="sxs-lookup"><span data-stu-id="7e900-111">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="7e900-112">Se você habilitar essa política, selecione um ou mais tamanhos de VM que podem ser criados no laboratório.</span><span class="sxs-lookup"><span data-stu-id="7e900-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="7e900-113">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7e900-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="7e900-114">Conjunto de máquinas virtuais por usuário</span><span class="sxs-lookup"><span data-stu-id="7e900-114">Set virtual machines per user</span></span>
<span data-ttu-id="7e900-115">Olá política para **máquinas virtuais por usuário** permite a você toospecify Olá alto número de máquinas virtuais que podem ser criados por um usuário individual.</span><span class="sxs-lookup"><span data-stu-id="7e900-115">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="7e900-116">Se um usuário tentar toocreate ou declaração de uma máquina virtual quando o limite de saudação do usuário foram atendido, uma mensagem de erro indica que Olá que VM não pode ser criado/exigida.</span><span class="sxs-lookup"><span data-stu-id="7e900-116">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="7e900-117">No laboratório de saudação **políticas e configurações** menu, selecione **máquinas virtuais por usuário**.</span><span class="sxs-lookup"><span data-stu-id="7e900-117">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Máquinas virtuais por usuário](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="7e900-119">Selecione **Sim** toolimit Olá diversas VMs por usuário.</span><span class="sxs-lookup"><span data-stu-id="7e900-119">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="7e900-120">Se você não quiser toolimit Olá diversas VMs por usuário, selecione **não**.</span><span class="sxs-lookup"><span data-stu-id="7e900-120">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="7e900-121">Se você selecionar **Sim**, insira um valor numérico que indica o número máximo de saudação de VMs que pode ser criado ou solicitado por um usuário.</span><span class="sxs-lookup"><span data-stu-id="7e900-121">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="7e900-122">Selecione **Sim** toolimit diversas Olá VMs que pode usar SSD (disco de estado sólido).</span><span class="sxs-lookup"><span data-stu-id="7e900-122">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="7e900-123">Se você não quiser toolimit diversas Olá VMs que pode usar o SSD, selecione **não**.</span><span class="sxs-lookup"><span data-stu-id="7e900-123">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="7e900-124">Se você selecionar **Sim**, insira um valor que indica o número máximo de saudação de máquinas virtuais que podem ser criados usando SSD.</span><span class="sxs-lookup"><span data-stu-id="7e900-124">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="7e900-125">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7e900-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="7e900-126">Conjunto de máquinas virtuais por laboratório</span><span class="sxs-lookup"><span data-stu-id="7e900-126">Set virtual machines per lab</span></span>
<span data-ttu-id="7e900-127">Olá política para **máquinas virtuais por laboratório** permite que você toospecify Olá número de máquinas virtuais que podem ser criados para o laboratório atual hello.</span><span class="sxs-lookup"><span data-stu-id="7e900-127">hello policy for **Virtual machines per lab** allows you toospecify hello maximum number of VMs that can be created for hello current lab.</span></span> <span data-ttu-id="7e900-128">Se um usuário tentar toocreate uma VM quando o limite de laboratório Olá foram atendido, uma mensagem de erro indica que Olá que VM não pode ser criada.</span><span class="sxs-lookup"><span data-stu-id="7e900-128">If a user attempts toocreate a VM when hello lab limit has been met, an error message indicates that hello VM cannot be created.</span></span> 

1. <span data-ttu-id="7e900-129">No laboratório de saudação **políticas e configurações** menu, selecione **máquinas virtuais por laboratório**.</span><span class="sxs-lookup"><span data-stu-id="7e900-129">On hello lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Máquinas virtuais por laboratório](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="7e900-131">Selecione **Sim** toolimit Olá diversas VMs por laboratório.</span><span class="sxs-lookup"><span data-stu-id="7e900-131">Select **Yes** toolimit hello number of VMs per lab.</span></span> <span data-ttu-id="7e900-132">Se você não quiser toolimit Olá diversas VMs por laboratório, selecione **não**.</span><span class="sxs-lookup"><span data-stu-id="7e900-132">If you do not want toolimit hello number of VMs per lab, select **No**.</span></span> <span data-ttu-id="7e900-133">Se você selecionar **Sim**, insira um valor numérico que indica o número máximo de saudação de VMs que pode ser criado ou solicitado por um usuário.</span><span class="sxs-lookup"><span data-stu-id="7e900-133">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="7e900-134">Selecione **Sim** toolimit diversas Olá VMs que pode usar SSD (disco de estado sólido).</span><span class="sxs-lookup"><span data-stu-id="7e900-134">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="7e900-135">Se você não quiser toolimit diversas Olá VMs que pode usar o SSD, selecione **não**.</span><span class="sxs-lookup"><span data-stu-id="7e900-135">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="7e900-136">Se você selecionar **Sim**, insira um valor que indica o número máximo de saudação de máquinas virtuais que podem ser criados usando SSD.</span><span class="sxs-lookup"><span data-stu-id="7e900-136">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="7e900-137">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7e900-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="7e900-138">Definir desligamento automático</span><span class="sxs-lookup"><span data-stu-id="7e900-138">Set auto-shutdown</span></span>
<span data-ttu-id="7e900-139">política de desligamento automático de saudação ajuda toominimize laboratório desperdiçar, permitindo que você tenha tempo de saudação toospecify que VMs deste laboratório desligadas.</span><span class="sxs-lookup"><span data-stu-id="7e900-139">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="7e900-140">No laboratório de saudação **políticas e configurações** folha, selecione **desligamento automático**.</span><span class="sxs-lookup"><span data-stu-id="7e900-140">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Desligamento automático](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="7e900-142">Selecione **na** tooenable essa política, e **Off** toodisable-lo.</span><span class="sxs-lookup"><span data-stu-id="7e900-142">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="7e900-143">Se você habilitar essa política, especifique Olá tooshut de tempo (e o fuso horário) para todas as máquinas virtuais no laboratório atual hello.</span><span class="sxs-lookup"><span data-stu-id="7e900-143">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="7e900-144">Especifique **Sim** ou **não** para Olá opção toosend uma toohello anterior de 15 minutos de notificação especificado o tempo de desligamento automático.</span><span class="sxs-lookup"><span data-stu-id="7e900-144">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="7e900-145">Se você especificar **Sim**, insira uma notificação de saudação tooreceive de ponto de extremidade do webhook URL.</span><span class="sxs-lookup"><span data-stu-id="7e900-145">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="7e900-146">Para saber mais sobre os webhooks, veja [Criar um webhook ou uma função da API do Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="7e900-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="7e900-147">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7e900-147">Select **Save**.</span></span>

    <span data-ttu-id="7e900-148">Por padrão, uma vez habilitada, essa diretiva se aplica a tooall VMs no laboratório atual hello.</span><span class="sxs-lookup"><span data-stu-id="7e900-148">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="7e900-149">tooremove essa configuração de uma VM específica, abra da VM Olá folha e altere seu **desligamento automático** configuração</span><span class="sxs-lookup"><span data-stu-id="7e900-149">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="7e900-150">Definir início automático</span><span class="sxs-lookup"><span data-stu-id="7e900-150">Set auto-start</span></span>
<span data-ttu-id="7e900-151">política de início automático Olá permite toospecify quando Olá máquinas virtuais no laboratório atual Olá deve ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="7e900-151">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="7e900-152">No laboratório de saudação **políticas e configurações** folha, selecione **Auto-start**.</span><span class="sxs-lookup"><span data-stu-id="7e900-152">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Início automático](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="7e900-154">Selecione **na** tooenable essa política, e **Off** toodisable-lo.</span><span class="sxs-lookup"><span data-stu-id="7e900-154">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="7e900-155">Se você habilitar essa política, especifique a hora de início agendada de saudação, fuso horário e Olá dias da semana Olá para qual Olá tempo se aplica.</span><span class="sxs-lookup"><span data-stu-id="7e900-155">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="7e900-156">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="7e900-156">Select **Save**.</span></span>

    <span data-ttu-id="7e900-157">Uma vez habilitada, essa política não é aplicada automaticamente tooany VMs no laboratório atual Olá.</span><span class="sxs-lookup"><span data-stu-id="7e900-157">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="7e900-158">tooapply tooa essa configuração VM específica, folha e alteração da VM Olá abrir seu **Auto-start** configuração</span><span class="sxs-lookup"><span data-stu-id="7e900-158">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="7e900-159">Definir a data de validade</span><span class="sxs-lookup"><span data-stu-id="7e900-159">Set expiration date</span></span>
<span data-ttu-id="7e900-160">Você pode definir uma expiração de data em que você [criar hello VM](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="7e900-160">You can set an expiration date when you [create hello VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="7e900-161">Em **configurações avançadas**, escolha Olá Calendário ícone toospecify uma data na qual Olá VM será excluída automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7e900-161">In **Advanced settings**, choose hello calendar icon toospecify a date on which hello VM will be automatically deleted.</span></span>  <span data-ttu-id="7e900-162">Por padrão, a saudação VM nunca expirará.</span><span class="sxs-lookup"><span data-stu-id="7e900-162">By default, hello VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="7e900-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7e900-163">Next steps</span></span>
<span data-ttu-id="7e900-164">Depois de definido e aplicado Olá várias configurações de política VM para o laboratório, aqui estão algumas coisas tootry lado:</span><span class="sxs-lookup"><span data-stu-id="7e900-164">Once you've defined and applied hello various VM policy settings for your lab, here are some things tootry next:</span></span>

* <span data-ttu-id="7e900-165">[Entender os endereços IP compartilhados](devtest-lab-shared-ip.md) -explica como compartilhado IP endereços são usados no número de saudação do DevTest Labs toominimize público IP endereços tooconnect necessária tooyour do laboratório de VMs.</span><span class="sxs-lookup"><span data-stu-id="7e900-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs toominimize hello number of public IP addresses required tooconnect tooyour lab VMs.</span></span>
* <span data-ttu-id="7e900-166">[Configurar o gerenciamento de custo](devtest-lab-configure-cost-management.md) -ilustra como Olá toouse **tendência mensal de custo estimado** gráfico</span><span class="sxs-lookup"><span data-stu-id="7e900-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how toouse hello **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="7e900-167">tooview Olá estimado custo acumulado do mês atual e o custo de final de mês de Olá projetado.</span><span class="sxs-lookup"><span data-stu-id="7e900-167">tooview hello current month's estimated cost-to-date and hello projected end-of-month cost.</span></span>
* <span data-ttu-id="7e900-168">[Criar imagem personalizada](devtest-lab-create-template.md) – durante a criação de uma VM, você especifica uma base, que pode ser uma imagem personalizada ou uma imagem do Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7e900-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="7e900-169">Este artigo ilustra como toocreate um personalizado da imagem de um arquivo VHD.</span><span class="sxs-lookup"><span data-stu-id="7e900-169">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="7e900-170">[Configurar imagens do Marketplace](devtest-lab-configure-marketplace-images.md) – O Azure DevTest Labs dá suporte à criação de VMs com base em imagens do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7e900-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="7e900-171">Este artigo ilustra como toospecify que, se houver, imagens do Azure Marketplace podem ser usado ao criar máquinas virtuais em um laboratório.</span><span class="sxs-lookup"><span data-stu-id="7e900-171">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="7e900-172">[Criar uma máquina virtual em um laboratório](devtest-lab-add-vm-with-artifacts.md) -ilustra como toocreate uma VM por meio de uma imagem de base (ou personalizadas ou Marketplace) e como toowork com artefatos em sua VM.</span><span class="sxs-lookup"><span data-stu-id="7e900-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

