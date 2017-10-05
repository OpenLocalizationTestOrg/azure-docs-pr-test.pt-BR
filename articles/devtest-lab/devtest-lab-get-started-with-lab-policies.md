---
title: "Gerenciar as políticas básicas de laboratório no Azure DevTest Labs| Microsoft Docs"
description: "Saiba como definir algumas políticas básicas (configurações) para um laboratório no DevTest Labs"
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
ms.openlocfilehash: ed35d081b191ec41ed9e5970515057a4715c0d59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="3bf23-103">Gerenciar políticas básicas para um laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="3bf23-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="3bf23-104">O Azure DevTest Labs permite que você controle o custo e minimize o desperdício nos laboratórios gerenciando políticas (configurações) para cada laboratório.</span><span class="sxs-lookup"><span data-stu-id="3bf23-104">Azure DevTest Labs enables you to control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="3bf23-105">Neste artigo, você começa com políticas aprendendo como definir duas das políticas mais importantes - limitando o número de VMs (máquinas virtuais) que podem ser criadas ou declaradas por um único usuário e configurando o desligamento automático.</span><span class="sxs-lookup"><span data-stu-id="3bf23-105">In this article, you get started with policies by learning how to set two of the most critical policies - limiting the number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="3bf23-106">Para ver como definir cada política de laboratório, veja o artigo [Definir políticas de laboratório no Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="3bf23-106">To view how to set every lab policy, see the article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="3bf23-107">Acessar as políticas de laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="3bf23-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="3bf23-108">As etapas a seguir orientam você durante a definição de políticas para um laboratório no Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="3bf23-108">The following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="3bf23-109">Para exibir (e alterar) as políticas de um laboratório, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="3bf23-109">To view (and change) the policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="3bf23-110">Entre no [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="3bf23-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="3bf23-111">Selecione **Mais serviços** e selecione **Laboratórios de Desenvolvimento/Teste** na lista.</span><span class="sxs-lookup"><span data-stu-id="3bf23-111">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="3bf23-112">Na lista de laboratórios, selecione o laboratório desejado.</span><span class="sxs-lookup"><span data-stu-id="3bf23-112">From the list of labs, select the desired lab.</span></span>   

1. <span data-ttu-id="3bf23-113">Selecione **Configuração e políticas**.</span><span class="sxs-lookup"><span data-stu-id="3bf23-113">Select **Configuration and policies**.</span></span>

    ![Folha de configurações de política](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="3bf23-115">A folha **Configurações de políticas** contém um menu de configurações que você pode especificar.</span><span class="sxs-lookup"><span data-stu-id="3bf23-115">The **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="3bf23-116">Este artigo aborda somente as configurações de**Máquinas virtuais por usuário** e **Desligamento automático**.</span><span class="sxs-lookup"><span data-stu-id="3bf23-116">This article covers only the settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="3bf23-117">Para saber mais sobre o restante das configurações, consulte [Gerenciar todas as políticas de um laboratório no Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="3bf23-117">To learn about the remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="3bf23-118">Conjunto de máquinas virtuais por usuário</span><span class="sxs-lookup"><span data-stu-id="3bf23-118">Set virtual machines per user</span></span>
<span data-ttu-id="3bf23-119">A política de **Máquinas virtuais por usuário** permite que você especifique o número máximo de VMs que podem ser criadas por um usuário individual.</span><span class="sxs-lookup"><span data-stu-id="3bf23-119">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="3bf23-120">Se um usuário tentar criar ou reivindicar uma VM quando o limite de usuários for atingido, uma mensagem de erro indicará que a VM não poderá ser criada/reivindicada.</span><span class="sxs-lookup"><span data-stu-id="3bf23-120">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="3bf23-121">No menu **Configuração e políticas** do laboratório, selecione **Máquinas virtuais por usuário**.</span><span class="sxs-lookup"><span data-stu-id="3bf23-121">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Máquinas virtuais por usuário](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="3bf23-123">Selecione **Sim** para limitar o número de VMs por usuário.</span><span class="sxs-lookup"><span data-stu-id="3bf23-123">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="3bf23-124">Se você não quiser limitar o número de VMs por usuário, selecione **Não**.</span><span class="sxs-lookup"><span data-stu-id="3bf23-124">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="3bf23-125">Se você selecionar **Sim**, insira um valor numérico indicando o número máximo de VMs que podem ser criadas ou reivindicadas por um usuário.</span><span class="sxs-lookup"><span data-stu-id="3bf23-125">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="3bf23-126">Selecione **Sim** para limitar o número de VMs que podem usar o SSD (disco de estado sólido).</span><span class="sxs-lookup"><span data-stu-id="3bf23-126">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="3bf23-127">Se você não quiser limitar o número de VMs que podem usar o SSD, selecione **Não**.</span><span class="sxs-lookup"><span data-stu-id="3bf23-127">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="3bf23-128">Se você selecionar **Sim**, insira um valor indicando o número máximo de VMs que podem ser criadas usando SSD.</span><span class="sxs-lookup"><span data-stu-id="3bf23-128">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="3bf23-129">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3bf23-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="3bf23-130">Definir desligamento automático</span><span class="sxs-lookup"><span data-stu-id="3bf23-130">Set auto-shutdown</span></span>
<span data-ttu-id="3bf23-131">A política de desligamento automático ajuda a minimizar o desperdício de laboratório, permitindo que você especifique a hora em que as VMs desse laboratório serão desligadas.</span><span class="sxs-lookup"><span data-stu-id="3bf23-131">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="3bf23-132">Na folha **Configuração e políticas** do laboratório, selecione **Desligamento automático**.</span><span class="sxs-lookup"><span data-stu-id="3bf23-132">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Desligamento automático](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="3bf23-134">Selecione **Ativado** para habilitar essa política e **Desativado** para desabilitá-la.</span><span class="sxs-lookup"><span data-stu-id="3bf23-134">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="3bf23-135">Se você habilitar essa política, especifique a hora (e fuso horário) para desligar todas as VMs no laboratório atual.</span><span class="sxs-lookup"><span data-stu-id="3bf23-135">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="3bf23-136">Especifique **Sim** ou **Não** para a opção de enviar uma notificação 15 minutos antes do tempo de desligamento automático especificado.</span><span class="sxs-lookup"><span data-stu-id="3bf23-136">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="3bf23-137">Se você especificar **Sim**, insira um ponto de extremidade de URL de webhook para receber a notificação.</span><span class="sxs-lookup"><span data-stu-id="3bf23-137">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="3bf23-138">Para saber mais sobre os webhooks, veja [Criar um webhook ou uma função da API do Azure](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="3bf23-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="3bf23-139">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3bf23-139">Select **Save**.</span></span>

    <span data-ttu-id="3bf23-140">Por padrão, uma vez habilitada, essa política se aplicará a todas as VMs do laboratório atual.</span><span class="sxs-lookup"><span data-stu-id="3bf23-140">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="3bf23-141">Para remover essa configuração de uma VM específica, abra a folha da VM e altere sua configuração de **Desligamento Automático**</span><span class="sxs-lookup"><span data-stu-id="3bf23-141">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="3bf23-142">Definir início automático</span><span class="sxs-lookup"><span data-stu-id="3bf23-142">Set auto-start</span></span>
<span data-ttu-id="3bf23-143">A política de início automático permite que você especifique quando as VMs do laboratório atual deverão ser iniciadas.</span><span class="sxs-lookup"><span data-stu-id="3bf23-143">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="3bf23-144">Na folha **Configuração e políticas** do laboratório, selecione **Início automático**.</span><span class="sxs-lookup"><span data-stu-id="3bf23-144">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Início automático](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="3bf23-146">Selecione **Ativado** para habilitar essa política e **Desativado** para desabilitá-la.</span><span class="sxs-lookup"><span data-stu-id="3bf23-146">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="3bf23-147">Se você habilitar esta política, especifique o horário de início agendado, o fuso horário e os dias da semana para os quais o horário se aplica.</span><span class="sxs-lookup"><span data-stu-id="3bf23-147">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="3bf23-148">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3bf23-148">Select **Save**.</span></span>

    <span data-ttu-id="3bf23-149">Quando habilitada, essa política não será aplicada automaticamente a quaisquer máquinas virtuais do laboratório atual.</span><span class="sxs-lookup"><span data-stu-id="3bf23-149">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="3bf23-150">Para aplicar essa configuração a uma VM específica, abra a folha da VM e altere sua configuração de **Início automático**</span><span class="sxs-lookup"><span data-stu-id="3bf23-150">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3bf23-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3bf23-151">Next steps</span></span>

- <span data-ttu-id="3bf23-152">[Definir políticas de laboratório no Azure DevTest Labs](devtest-lab-set-lab-policy.md) - saiba como modificar outras políticas de laboratório</span><span class="sxs-lookup"><span data-stu-id="3bf23-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how to modify other lab policies</span></span> 
