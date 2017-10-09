---
title: "atualizações do sistema aaaApply na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendações da Central de segurança do Azure * * aplicar atualizações de sistema * * e * * reinicializar após as atualizações de sistema * *."
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
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a><span data-ttu-id="04948-103">Aplicar atualizações do sistema na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="04948-103">Apply system updates in Azure Security Center</span></span>
<span data-ttu-id="04948-104">A Central de Segurança do Azure monitora diariamente VMs (máquinas virtuais) Windows e Linux para saber se faltam atualizações do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="04948-104">Azure Security Center monitors daily Windows and  Linux virtual machines (VMs) for missing operating system updates.</span></span> <span data-ttu-id="04948-105">A Central de Segurança recupera uma lista de atualizações críticas e de segurança disponíveis no Windows Update ou no WSUS (Windows Server Update Services), dependendo de qual serviço está configurado em uma VM do Windows.</span><span class="sxs-lookup"><span data-stu-id="04948-105">Security Center retrieves a list of available security and critical updates from Windows Update or Windows Server Update Services (WSUS), depending on which service is configured on a Windows VM.</span></span>  <span data-ttu-id="04948-106">Central de segurança também verifica as atualizações mais recentes de saudação em sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="04948-106">Security Center also checks for hello latest updates in Linux systems.</span></span> <span data-ttu-id="04948-107">Se faltar uma atualização do sistema em sua VM, a Central de Segurança recomendará que você aplique as atualizações do sistema</span><span class="sxs-lookup"><span data-stu-id="04948-107">If your VM is missing a system update, Security Center will recommend that you apply system updates</span></span>

> [!NOTE]
> <span data-ttu-id="04948-108">Este documento apresenta serviço hello usando um exemplo de implantação.</span><span class="sxs-lookup"><span data-stu-id="04948-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="04948-109">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="04948-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="04948-110">Implementar a recomendação de saudação</span><span class="sxs-lookup"><span data-stu-id="04948-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="04948-111">Em Olá **recomendações** folha, selecione **aplicar atualizações do sistema**.</span><span class="sxs-lookup"><span data-stu-id="04948-111">In hello **Recommendations** blade, select **Apply system updates**.</span></span>

   ![Aplicar atualizações do sistema][1]
2. <span data-ttu-id="04948-113">Olá **aplicar atualizações do sistema** folha é aberta exibindo uma lista de VMs com atualizações de sistema ausentes.</span><span class="sxs-lookup"><span data-stu-id="04948-113">hello **Apply system updates** blade opens displaying a list of VMs missing system updates.</span></span> <span data-ttu-id="04948-114">Selecionar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="04948-114">Select a VM.</span></span>

   ![Selecionar uma máquina virtual][2]
3. <span data-ttu-id="04948-116">Uma folha abrirá exibindo uma lista de atualizações ausentes para a VM.</span><span class="sxs-lookup"><span data-stu-id="04948-116">A blade opens displaying a list of missing updates for that VM.</span></span> <span data-ttu-id="04948-117">Selecione uma atualização do sistema.</span><span class="sxs-lookup"><span data-stu-id="04948-117">Select a system update.</span></span> <span data-ttu-id="04948-118">Neste exemplo, vamos selecionar KB3156016.</span><span class="sxs-lookup"><span data-stu-id="04948-118">In this example, let’s select KB3156016.</span></span>

   ![Atualizações de segurança ausentes][3]

4. <span data-ttu-id="04948-120">Siga as etapas de Olá Olá **de atualização de segurança** tooapply folha Olá atualização ausente.</span><span class="sxs-lookup"><span data-stu-id="04948-120">Follow hello steps in hello **Security Update** blade tooapply hello missing update.</span></span>

   ![Atualização de segurança][4]

## <a name="reboot-after-system-updates"></a><span data-ttu-id="04948-122">Reinicializar após as atualizações do sistema</span><span class="sxs-lookup"><span data-stu-id="04948-122">Reboot after system updates</span></span>
1. <span data-ttu-id="04948-123">Retornar toohello **recomendações** folha.</span><span class="sxs-lookup"><span data-stu-id="04948-123">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="04948-124">Uma nova entrada foi gerada depois que você aplicou atualizações do sistema, chamada **Reinicializar após as atualizações do sistema**.</span><span class="sxs-lookup"><span data-stu-id="04948-124">A new entry was generated after you applied system updates, called **Reboot after system updates**.</span></span> <span data-ttu-id="04948-125">Essa entrada permite que você saiba o que você precisa que o processo de saudação tooreboot Olá VM toocomplete de aplicação de atualizações do sistema.</span><span class="sxs-lookup"><span data-stu-id="04948-125">This entry lets you know that you need tooreboot hello VM toocomplete hello process of applying system updates.</span></span>

   ![Reinicializar após as atualizações do sistema][5]
2. <span data-ttu-id="04948-127">Selecione **Reinicializar após as atualizações do sistema**.</span><span class="sxs-lookup"><span data-stu-id="04948-127">Select **Reboot after system updates**.</span></span> <span data-ttu-id="04948-128">Isso abre **uma reinicialização está pendente toocomplete atualizações do sistema** folha exibindo uma lista de máquinas virtuais que você precisa toorestart toocomplete Olá aplica o processo de atualizações do sistema.</span><span class="sxs-lookup"><span data-stu-id="04948-128">This opens **A restart is pending toocomplete system updates** blade displaying a list of VMs that you need toorestart toocomplete hello apply system updates process.</span></span>

   ![Reinicialização pendente][6]

<span data-ttu-id="04948-130">Reinicie Olá VM do processo de saudação toocomplete do Azure.</span><span class="sxs-lookup"><span data-stu-id="04948-130">Restart hello VM from Azure toocomplete hello process.</span></span>

## <a name="see-also"></a><span data-ttu-id="04948-131">Consulte também</span><span class="sxs-lookup"><span data-stu-id="04948-131">See also</span></span>
<span data-ttu-id="04948-132">toolearn mais sobre o Centro de segurança, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="04948-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="04948-133">[Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="04948-133">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="04948-134">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="04948-134">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="04948-135">[Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="04948-135">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="04948-136">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="04948-136">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="04948-137">[Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="04948-137">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="04948-138">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="04948-138">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="04948-139">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="04948-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
