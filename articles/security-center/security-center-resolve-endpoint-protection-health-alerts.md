---
title: "Resolver alertas de integridade do Endpoint Protection na Central de segurança do Azure| Microsoft Docs"
description: "Este documento mostra como implementar a recomendação da Central de Segurança do Azure para **Resolver alertas de integridade do Endpoint Protection**."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 5e6b136d6bd3b11fb82126d104fd0cb149255118
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="39d53-103">Resolver alertas de integridade do Endpoint Protection na Central de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="39d53-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="39d53-104">A Central de Segurança do Azure recomendará que você resolva os alertas de integridade do Endpoint Protection detectados.</span><span class="sxs-lookup"><span data-stu-id="39d53-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="39d53-105">A Central de Segurança permite que você veja quais máquinas virtuais (VMs) têm falhas do Endpoint Protection e saiba a quantidade de falhas.</span><span class="sxs-lookup"><span data-stu-id="39d53-105">Security Center enables you to see which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="39d53-106">Este documento apresenta o serviço usando uma implantação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="39d53-106">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="39d53-107">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="39d53-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-the-recommendation"></a><span data-ttu-id="39d53-108">Implementar a recomendação</span><span class="sxs-lookup"><span data-stu-id="39d53-108">Implement the recommendation</span></span>
1. <span data-ttu-id="39d53-109">Na **folha Recomendações**, selecione **Resolver alertas de integridade do Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="39d53-109">In the **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="39d53-110">![Resolver alertas de integridade de proteção do ponto de extremidade][1]</span><span class="sxs-lookup"><span data-stu-id="39d53-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="39d53-111">Isso abrirá a folha **Falha no Endpoint Protection** , que lista as VMs com falhas e o número de falhas para cada VM.</span><span class="sxs-lookup"><span data-stu-id="39d53-111">This opens the blade **Endpoint Protection failure** which lists VMs with failures and the number of failures for each VM.</span></span> <span data-ttu-id="39d53-112">Selecione uma VM na lista.</span><span class="sxs-lookup"><span data-stu-id="39d53-112">Select a VM from the list.</span></span>
   <span data-ttu-id="39d53-113">![Endpoint protection failure][2]</span><span class="sxs-lookup"><span data-stu-id="39d53-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="39d53-114">Uma folha **Lista de Falhas** é aberta para a VM selecionada, exibindo uma lista de falhas.</span><span class="sxs-lookup"><span data-stu-id="39d53-114">A **Failures List** blade opens for the selected VM, displaying a list of failures.</span></span> <span data-ttu-id="39d53-115">Selecione uma falha na lista para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="39d53-115">Select a failure from the list to learn more.</span></span> <span data-ttu-id="39d53-116">Isso abre uma folha com informações sobre a falha selecionada.</span><span class="sxs-lookup"><span data-stu-id="39d53-116">This opens a blade with information about the selected failure.</span></span>
   <span data-ttu-id="39d53-117">![Lista de falhas][3]
   ![Eventos de falha][4]</span><span class="sxs-lookup"><span data-stu-id="39d53-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="39d53-118">Consulte também</span><span class="sxs-lookup"><span data-stu-id="39d53-118">See also</span></span>
<span data-ttu-id="39d53-119">Para saber mais sobre a Central de Segurança, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="39d53-119">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="39d53-120">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md): saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="39d53-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="39d53-121">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="39d53-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="39d53-122">[Monitoramento de integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md): saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="39d53-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="39d53-123">[Gerenciar e responder aos alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md): aprenda a gerenciar e responder aos alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="39d53-123">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="39d53-124">[Monitorar as soluções de parceiros com a Central de Segurança do Azure](security-center-partner-solutions.md) : saiba como monitorar o status de integridade de suas soluções de parceiros.</span><span class="sxs-lookup"><span data-stu-id="39d53-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="39d53-125">[Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md): encontre perguntas frequentes sobre como usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="39d53-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="39d53-126">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/): obtenha as últimas notícias de segurança e informações do Azure.</span><span class="sxs-lookup"><span data-stu-id="39d53-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
