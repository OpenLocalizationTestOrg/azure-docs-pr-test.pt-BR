---
title: "Aplicar atualizações do sistema na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento mostra como implementar as recomendações da Central de Segurança do Azure **Aplicar atualizações do sistema** e **Reinicializar após as atualizações do sistema**."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 50cdea437db5387813c6a3905d14b6904d2aba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="71e51-103">Aplicar atualizações do sistema na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="71e51-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="71e51-104">A Central de Segurança do Azure monitora diariamente VMs (máquinas virtuais) Windows e Linux para saber se faltam atualizações do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="71e51-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="71e51-105">A Central de Segurança recupera uma lista de atualizações críticas e de segurança disponíveis no Windows Update ou no WSUS (Windows Server Update Services), dependendo de qual serviço está configurado em uma VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="71e51-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="71e51-106">A Central de Segurança também verifica as atualizações mais recentes em sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="71e51-106">Security Center also checks for the latest updates in Linux systems.</span></span> <span data-ttu-id="71e51-107">Se faltar uma atualização do sistema em sua VM, a Central de Segurança recomendará que você aplique as atualizações do sistema</span><span class="sxs-lookup"><span data-stu-id="71e51-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="71e51-108">Este documento apresenta o serviço usando uma implantação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="71e51-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="71e51-109">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="71e51-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="71e51-110">Implementar a recomendação</span><span class="sxs-lookup"><span data-stu-id="71e51-110">Implement the recommendation</span></span>
1. <span data-ttu-id="71e51-111">Na folha **Recomendações**, selecione **Aplicar atualizações do sistema**.</span><span class="sxs-lookup"><span data-stu-id="71e51-111">In the **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Aplicar atualizações do sistema][1]
2. <span data-ttu-id="71e51-113">A folha **Aplicar atualizações do sistema** abre exibindo uma lista de VMs sem atualizações de sistema.</span><span class="sxs-lookup"><span data-stu-id="71e51-113">The **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="71e51-114">Selecione uma VM.</span><span class="sxs-lookup"><span data-stu-id="71e51-114">Select a VM.</span></span>

   ![Selecionar uma máquina virtual][2]
3. <span data-ttu-id="71e51-116">Uma folha abrirá exibindo uma lista de atualizações ausentes para a VM.</span><span class="sxs-lookup"><span data-stu-id="71e51-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="71e51-117">Selecione uma atualização do sistema.</span><span class="sxs-lookup"><span data-stu-id="71e51-117">Select a system update.</span></span> <span data-ttu-id="71e51-118">Neste exemplo, vamos selecionar KB3156016.</span><span class="sxs-lookup"><span data-stu-id="71e51-118">In this example, let’s select KB3156016.</span></span>

   ![Atualizações de segurança ausentes][3]

4. <span data-ttu-id="71e51-120">Siga as etapas na folha **Atualização de segurança** para aplicar a atualização ausente.</span><span class="sxs-lookup"><span data-stu-id="71e51-120">Follow the steps in the **Security Update** blade to apply the missing update.</span></span>

   ![Atualização de segurança][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="71e51-122">Reinicializar após as atualizações do sistema</span><span class="sxs-lookup"><span data-stu-id="71e51-122">Reboot after system updates</span></span>
1. <span data-ttu-id="71e51-123">Volte para a folha **Recomendações** .</span><span class="sxs-lookup"><span data-stu-id="71e51-123">Return to the **Recommendations** blade.</span></span> <span data-ttu-id="71e51-124">Uma nova entrada foi gerada depois que você aplicou atualizações do sistema, chamada **Reinicializar após as atualizações do sistema**.</span><span class="sxs-lookup"><span data-stu-id="71e51-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="71e51-125">Essa entrada permite que você saiba que é necessário reinicializar a máquina virtual para concluir o processo de aplicação de atualizações de sistema.</span><span class="sxs-lookup"><span data-stu-id="71e51-125">This entry lets you know that you need to reboot the VM to complete the process of applying system updates.</span></span>

   ![Reinicializar após as atualizações do sistema][5]
2. <span data-ttu-id="71e51-127">Selecione **Reinicializar após as atualizações do sistema**.</span><span class="sxs-lookup"><span data-stu-id="71e51-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="71e51-128">Isso abre a folha **Uma reinicialização está pendente para concluir as atualizações do sistema** exibindo uma lista de máquinas virtuais que você precisa reiniciar para concluir o processo de aplicar atualizações d sistema.</span><span class="sxs-lookup"><span data-stu-id="71e51-128">This opens **A restart is pending to complete system updates** blade displaying a list of VMs that you need to restart to complete the apply system updates process.</span></span>

   ![Reinicialização pendente][6]

<span data-ttu-id="71e51-130">Reinicie a VM do Azure para concluir o processo.</span><span class="sxs-lookup"><span data-stu-id="71e51-130">Restart the VM from Azure to complete the process.</span></span>

## <a name="see-also"></a><span data-ttu-id="71e51-131">Consulte também</span><span class="sxs-lookup"><span data-stu-id="71e51-131">See also</span></span>
<span data-ttu-id="71e51-132">Para saber mais sobre a Central de Segurança, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="71e51-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="71e51-133">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md) – saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="71e51-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="71e51-134">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="71e51-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="71e51-135">[Monitoramento de integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md) : saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="71e51-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="71e51-136">[Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) : aprenda a gerenciar e a responder a alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="71e51-136">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="71e51-137">[Monitoramento de soluções de parceiros com a Central de Segurança do Azure](security-center-partner-solutions.md) – saiba como monitorar o status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="71e51-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="71e51-138">[Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md) : encontre as perguntas frequentes sobre como usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="71e51-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="71e51-139">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="71e51-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
