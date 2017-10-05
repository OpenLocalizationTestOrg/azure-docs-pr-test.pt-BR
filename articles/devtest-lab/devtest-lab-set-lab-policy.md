---
title: "Gerenciar políticas de laboratório no Azure DevTest Labs| Microsoft Docs"
description: "Aprenda a definir as políticas do laboratório, como os tamanhos das VMs, o número máximo de VMs por usuário e o desligamento automático."
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
ms.openlocfilehash: 328a4d893637d7150807855e118b485a2c3bbfc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="13e5d-103">Gerenciar todas as políticas de um laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="13e5d-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="13e5d-104">O Azure DevTest Labs permite controlar o custo e minimize o desperdício nos laboratórios gerenciando políticas (configurações) de cada laboratório.</span><span class="sxs-lookup"><span data-stu-id="13e5d-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="13e5d-105">Este artigo explica em detalhes passo a passo como definir cada política.</span><span class="sxs-lookup"><span data-stu-id="13e5d-105">This article explains in step-by-step detail how to set each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="13e5d-106">Definir tamanhos de máquina virtual permitidos</span><span class="sxs-lookup"><span data-stu-id="13e5d-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="13e5d-107">A política para definir os tamanhos de VM permitidos ajuda a minimizar o desperdício de laboratório, permitindo que você especifique quais tamanhos de VM são permitidos no laboratório.</span><span class="sxs-lookup"><span data-stu-id="13e5d-107">The policy for setting the allowed VM sizes helps to minimize lab waste by enabling you to specify which VM sizes are allowed in the lab.</span></span> <span data-ttu-id="13e5d-108">Quando essa política é ativada, somente os tamanhos de VM nesta lista podem ser usados para criar VMs.</span><span class="sxs-lookup"><span data-stu-id="13e5d-108">If this policy is activated, only VM sizes from this list can be used to create VMs.</span></span>

1. <span data-ttu-id="13e5d-109">Na folha **Configurações e políticas** do laboratório, selecione **Tamanhos de máquinas virtuais permitidos**.</span><span class="sxs-lookup"><span data-stu-id="13e5d-109">On the lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![Tamanhos de máquinas virtuais permitidos](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="13e5d-111">Selecione **Ativado** para habilitar essa política e **Desativado** para desabilitá-la.</span><span class="sxs-lookup"><span data-stu-id="13e5d-111">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="13e5d-112">Se você habilitar essa política, selecione um ou mais tamanhos de VM que podem ser criados no laboratório.</span><span class="sxs-lookup"><span data-stu-id="13e5d-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="13e5d-113">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="13e5d-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="13e5d-114">Conjunto de máquinas virtuais por usuário</span><span class="sxs-lookup"><span data-stu-id="13e5d-114">Set virtual machines per user</span></span>
<span data-ttu-id="13e5d-115">A política de **Máquinas virtuais por usuário** permite que você especifique o número máximo de VMs que podem ser criadas por um usuário individual.</span><span class="sxs-lookup"><span data-stu-id="13e5d-115">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="13e5d-116">Se um usuário tentar criar ou reivindicar uma VM quando o limite de usuários for atingido, uma mensagem de erro indicará que a VM não poderá ser criada/reivindicada.</span><span class="sxs-lookup"><span data-stu-id="13e5d-116">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="13e5d-117">No menu **Configuração e políticas** do laboratório, selecione **Máquinas virtuais por usuário**.</span><span class="sxs-lookup"><span data-stu-id="13e5d-117">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Máquinas virtuais por usuário](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="13e5d-119">Selecione **Sim** para limitar o número de VMs por usuário.</span><span class="sxs-lookup"><span data-stu-id="13e5d-119">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="13e5d-120">Se você não quiser limitar o número de VMs por usuário, selecione **Não**.</span><span class="sxs-lookup"><span data-stu-id="13e5d-120">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="13e5d-121">Se você selecionar **Sim**, insira um valor numérico indicando o número máximo de VMs que podem ser criadas ou reivindicadas por um usuário.</span><span class="sxs-lookup"><span data-stu-id="13e5d-121">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="13e5d-122">Selecione **Sim** para limitar o número de VMs que podem usar o SSD (disco de estado sólido).</span><span class="sxs-lookup"><span data-stu-id="13e5d-122">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="13e5d-123">Se você não quiser limitar o número de VMs que podem usar o SSD, selecione **Não**.</span><span class="sxs-lookup"><span data-stu-id="13e5d-123">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="13e5d-124">Se você selecionar **Sim**, insira um valor indicando o número máximo de VMs que podem ser criadas usando SSD.</span><span class="sxs-lookup"><span data-stu-id="13e5d-124">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="13e5d-125">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="13e5d-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="13e5d-126">Conjunto de máquinas virtuais por laboratório</span><span class="sxs-lookup"><span data-stu-id="13e5d-126">Set virtual machines per lab</span></span>
<span data-ttu-id="13e5d-127">A política de **Máquinas virtuais por laboratório** permite que você especifique o número máximo de VMs que podem ser criadas para o laboratório atual.</span><span class="sxs-lookup"><span data-stu-id="13e5d-127">The policy for **Virtual machines per lab** allows you to specify the maximum number of VMs that can be created for the current lab.</span></span> <span data-ttu-id="13e5d-128">Se um usuário tentar criar uma VM quando o limite de laboratórios for alcançado, uma mensagem de erro indicará que a VM não pode ser criada.</span><span class="sxs-lookup"><span data-stu-id="13e5d-128">If a user attempts to create a VM when the lab limit has been met, an error message indicates that the VM cannot be created.</span></span> 

1. <span data-ttu-id="13e5d-129">No menu **Configuração e políticas** do laboratório, selecione **Máquinas virtuais por laboratório**.</span><span class="sxs-lookup"><span data-stu-id="13e5d-129">On the lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Máquinas virtuais por laboratório](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="13e5d-131">Selecione **Sim** para limitar o número de VMs por laboratório.</span><span class="sxs-lookup"><span data-stu-id="13e5d-131">Select **Yes** to limit the number of VMs per lab.</span></span> <span data-ttu-id="13e5d-132">Se você não quiser limitar o número de VMs por laboratório, selecione **Não**.</span><span class="sxs-lookup"><span data-stu-id="13e5d-132">If you do not want to limit the number of VMs per lab, select **No**.</span></span> <span data-ttu-id="13e5d-133">Se você selecionar **Sim**, insira um valor numérico indicando o número máximo de VMs que podem ser criadas ou reivindicadas por um usuário.</span><span class="sxs-lookup"><span data-stu-id="13e5d-133">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="13e5d-134">Selecione **Sim** para limitar o número de VMs que podem usar o SSD (disco de estado sólido).</span><span class="sxs-lookup"><span data-stu-id="13e5d-134">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="13e5d-135">Se você não quiser limitar o número de VMs que podem usar o SSD, selecione **Não**.</span><span class="sxs-lookup"><span data-stu-id="13e5d-135">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="13e5d-136">Se você selecionar **Sim**, insira um valor indicando o número máximo de VMs que podem ser criadas usando SSD.</span><span class="sxs-lookup"><span data-stu-id="13e5d-136">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="13e5d-137">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="13e5d-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="13e5d-138">Definir desligamento automático</span><span class="sxs-lookup"><span data-stu-id="13e5d-138">Set auto-shutdown</span></span>
<span data-ttu-id="13e5d-139">A política de desligamento automático ajuda a minimizar o desperdício de laboratório, permitindo que você especifique a hora em que as VMs desse laboratório serão desligadas.</span><span class="sxs-lookup"><span data-stu-id="13e5d-139">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="13e5d-140">Na folha **Configuração e políticas** do laboratório, selecione **Desligamento automático**.</span><span class="sxs-lookup"><span data-stu-id="13e5d-140">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Desligamento automático](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="13e5d-142">Selecione **Ativado** para habilitar essa política e **Desativado** para desabilitá-la.</span><span class="sxs-lookup"><span data-stu-id="13e5d-142">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="13e5d-143">Se você habilitar essa política, especifique a hora (e fuso horário) para desligar todas as VMs no laboratório atual.</span><span class="sxs-lookup"><span data-stu-id="13e5d-143">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="13e5d-144">Especifique **Sim** ou **Não** para a opção de enviar uma notificação 15 minutos antes do tempo de desligamento automático especificado.</span><span class="sxs-lookup"><span data-stu-id="13e5d-144">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="13e5d-145">Se você especificar **Sim**, insira um ponto de extremidade de URL de webhook para receber a notificação.</span><span class="sxs-lookup"><span data-stu-id="13e5d-145">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="13e5d-146">Para saber mais sobre os webhooks, veja [Criar um webhook ou uma função da API do Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="13e5d-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="13e5d-147">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="13e5d-147">Select **Save**.</span></span>

    <span data-ttu-id="13e5d-148">Por padrão, uma vez habilitada, essa política se aplicará a todas as VMs do laboratório atual.</span><span class="sxs-lookup"><span data-stu-id="13e5d-148">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="13e5d-149">Para remover essa configuração de uma VM específica, abra a folha da VM e altere sua configuração de **Desligamento Automático**</span><span class="sxs-lookup"><span data-stu-id="13e5d-149">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="13e5d-150">Definir início automático</span><span class="sxs-lookup"><span data-stu-id="13e5d-150">Set auto-start</span></span>
<span data-ttu-id="13e5d-151">A política de início automático permite que você especifique quando as VMs do laboratório atual deverão ser iniciadas.</span><span class="sxs-lookup"><span data-stu-id="13e5d-151">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="13e5d-152">Na folha **Configuração e políticas** do laboratório, selecione **Início automático**.</span><span class="sxs-lookup"><span data-stu-id="13e5d-152">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Início automático](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="13e5d-154">Selecione **Ativado** para habilitar essa política e **Desativado** para desabilitá-la.</span><span class="sxs-lookup"><span data-stu-id="13e5d-154">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="13e5d-155">Se você habilitar esta política, especifique o horário de início agendado, o fuso horário e os dias da semana para os quais o horário se aplica.</span><span class="sxs-lookup"><span data-stu-id="13e5d-155">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="13e5d-156">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="13e5d-156">Select **Save**.</span></span>

    <span data-ttu-id="13e5d-157">Quando habilitada, essa política não será aplicada automaticamente a quaisquer máquinas virtuais do laboratório atual.</span><span class="sxs-lookup"><span data-stu-id="13e5d-157">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="13e5d-158">Para aplicar essa configuração a uma VM específica, abra a folha da VM e altere sua configuração de **Início automático**</span><span class="sxs-lookup"><span data-stu-id="13e5d-158">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="13e5d-159">Definir a data de validade</span><span class="sxs-lookup"><span data-stu-id="13e5d-159">Set expiration date</span></span>
<span data-ttu-id="13e5d-160">Você pode definir uma data de validade ao [criar a VM](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="13e5d-160">You can set an expiration date when you [create the VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="13e5d-161">Em **Configurações avançadas**, escolha o ícone de calendário para especificar uma data em que a VM será excluída automaticamente.</span><span class="sxs-lookup"><span data-stu-id="13e5d-161">In **Advanced settings**, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span></span>  <span data-ttu-id="13e5d-162">Por padrão, a VM nunca expirará.</span><span class="sxs-lookup"><span data-stu-id="13e5d-162">By default, the VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="13e5d-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="13e5d-163">Next steps</span></span>
<span data-ttu-id="13e5d-164">Depois de definir e aplicar as várias configurações da política de VM em seu laboratório, aqui estão algumas opções para você tentar em seguida:</span><span class="sxs-lookup"><span data-stu-id="13e5d-164">Once you've defined and applied the various VM policy settings for your lab, here are some things to try next:</span></span>

* <span data-ttu-id="13e5d-165">[Entender os endereços IP compartilhados](devtest-lab-shared-ip.md) - explica como os endereços IP compartilhados são usados no DevTest Labs para minimizar o número de endereços IP públicos necessárias para conectar-se às VMs de seu laboratório.</span><span class="sxs-lookup"><span data-stu-id="13e5d-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs to minimize the number of public IP addresses required to connect to your lab VMs.</span></span>
* <span data-ttu-id="13e5d-166">[Configurar o gerenciamento de custo](devtest-lab-configure-cost-management.md) – ilustra como usar o gráfico **Tendência de custo estimado mensal**</span><span class="sxs-lookup"><span data-stu-id="13e5d-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how to use the **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="13e5d-167">para exibir o custo até a data estimado do mês atual e o custo projetado do final de mês.</span><span class="sxs-lookup"><span data-stu-id="13e5d-167">to view the current month's estimated cost-to-date and the projected end-of-month cost.</span></span>
* <span data-ttu-id="13e5d-168">[Criar imagem personalizada](devtest-lab-create-template.md) – durante a criação de uma VM, você especifica uma base, que pode ser uma imagem personalizada ou uma imagem do Marketplace.</span><span class="sxs-lookup"><span data-stu-id="13e5d-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="13e5d-169">Este artigo ilustra como criar uma imagem personalizada de um arquivo VHD.</span><span class="sxs-lookup"><span data-stu-id="13e5d-169">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="13e5d-170">[Configurar imagens do Marketplace](devtest-lab-configure-marketplace-images.md) – O Azure DevTest Labs dá suporte à criação de VMs com base em imagens do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="13e5d-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="13e5d-171">Este artigo ilustra como especificar quais imagens (caso haja alguma) do Azure Marketplace podem ser usadas durante a criação de VMs em um laboratório.</span><span class="sxs-lookup"><span data-stu-id="13e5d-171">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="13e5d-172">[Criar uma VM em um laboratório](devtest-lab-add-vm-with-artifacts.md) – ilustra como criar uma VM de uma imagem base (personalizada ou do Marketplace) e como trabalhar com artefatos na VM.</span><span class="sxs-lookup"><span data-stu-id="13e5d-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

