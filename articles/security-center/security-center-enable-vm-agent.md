---
title: "aaaEnable agente de VM na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * habilitar o VM Agent * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="82190-103">Habilitar o Agente de VM na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="82190-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="82190-104">Olá VM Agent deve ser instalado em máquinas virtuais (VMs) na ordem muito[habilitar coleta de dados](security-center-enable-data-collection.md).</span><span class="sxs-lookup"><span data-stu-id="82190-104">hello VM Agent must be installed on virtual machines (VMs) in order too[enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="82190-105">Habilita a Central de segurança do Azure você toosee que exigem VMs Olá agente de VM e recomendará que você habilite Olá agente de VM nessas VMs.</span><span class="sxs-lookup"><span data-stu-id="82190-105">Azure Security Center enables you toosee which VMs require hello VM Agent and will recommend that you enable hello VM Agent on those VMs.</span></span>

<span data-ttu-id="82190-106">Olá agente VM é instalado por padrão para VMs que são implantados de saudação do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="82190-106">hello VM Agent is installed by default for VMs that are deployed from hello Azure Marketplace.</span></span> <span data-ttu-id="82190-107">artigo Olá [agente de VM e extensões – parte 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) fornece informações sobre como tooinstall Olá agente de VM.</span><span class="sxs-lookup"><span data-stu-id="82190-107">hello article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how tooinstall hello VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="82190-108">Este documento apresenta serviço hello usando um exemplo de implantação.</span><span class="sxs-lookup"><span data-stu-id="82190-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="82190-109">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="82190-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="82190-110">Implementar a recomendação de saudação</span><span class="sxs-lookup"><span data-stu-id="82190-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="82190-111">Em Olá **folha recomendações**, selecione **habilitar o agente de VM**.</span><span class="sxs-lookup"><span data-stu-id="82190-111">In hello **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="82190-112">![Habilitar o Agente de VM][1]</span><span class="sxs-lookup"><span data-stu-id="82190-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="82190-113">Isso abre a folha de saudação **VM Agent está ausente ou não respondendo**.</span><span class="sxs-lookup"><span data-stu-id="82190-113">This opens hello blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="82190-114">Esta folha lista Olá máquinas virtuais que exigem Olá agente de VM.</span><span class="sxs-lookup"><span data-stu-id="82190-114">This blade lists hello VMs that require hello VM Agent.</span></span> <span data-ttu-id="82190-115">Siga as instruções de saudação no agente de VM Olá folha tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="82190-115">Follow hello instructions on hello blade tooinstall hello VM agent.</span></span>
   <span data-ttu-id="82190-116">![O Agente de VM está ausente][2]</span><span class="sxs-lookup"><span data-stu-id="82190-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="82190-117">Consulte também</span><span class="sxs-lookup"><span data-stu-id="82190-117">See also</span></span>
<span data-ttu-id="82190-118">toolearn mais sobre o Centro de segurança, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="82190-118">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="82190-119">[Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md)– Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="82190-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="82190-120">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="82190-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="82190-121">[Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md)– Saiba como toomonitor Olá a integridade de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="82190-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="82190-122">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md)– Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="82190-122">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="82190-123">[Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="82190-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="82190-124">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md)– localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="82190-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="82190-125">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/)– obter notícias mais recentes de segurança do Azure hello e informações.</span><span class="sxs-lookup"><span data-stu-id="82190-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
