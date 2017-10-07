---
title: "alertas de integridade de proteção de ponto de extremidade de aaaResolve na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * resolver Endpoint Protection integridade alertas * *."
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
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a><span data-ttu-id="bf51f-103">Resolver alertas de integridade do Endpoint Protection na Central de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="bf51f-103">Resolve endpoint protection health alerts in Azure Security Center</span></span>
<span data-ttu-id="bf51f-104">A Central de Segurança do Azure recomendará que você resolva os alertas de integridade do Endpoint Protection detectados.</span><span class="sxs-lookup"><span data-stu-id="bf51f-104">Azure Security Center will recommend that you resolve detected endpoint protection health alerts.</span></span>  <span data-ttu-id="bf51f-105">Central de segurança permite que você toosee quais máquinas virtuais (VMs) têm falhas de proteção de ponto de extremidade e quantos.</span><span class="sxs-lookup"><span data-stu-id="bf51f-105">Security Center enables you toosee which virtual machines (VMs) have endpoint protection failures and how many failures.</span></span>

> [!NOTE]
> <span data-ttu-id="bf51f-106">Este documento apresenta serviço hello usando um exemplo de implantação.</span><span class="sxs-lookup"><span data-stu-id="bf51f-106">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="bf51f-107">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="bf51f-107">This is not a step-by-step guide.</span></span>
> 
> 

## <a name="implement-hello-recommendation"></a><span data-ttu-id="bf51f-108">Implementar a recomendação de saudação</span><span class="sxs-lookup"><span data-stu-id="bf51f-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="bf51f-109">Em Olá **folha recomendações**, selecione **alertas de integridade de proteção de ponto de extremidade resolver**.</span><span class="sxs-lookup"><span data-stu-id="bf51f-109">In hello **Recommendations blade**, select **Resolve Endpoint Protection health alerts**.</span></span>
   <span data-ttu-id="bf51f-110">![Resolver alertas de integridade de proteção do ponto de extremidade][1]</span><span class="sxs-lookup"><span data-stu-id="bf51f-110">![Resolve endpoint protection health alerts][1]</span></span>
2. <span data-ttu-id="bf51f-111">Isso abre a folha de saudação **Falha na proteção de ponto de extremidade** que lista as máquinas virtuais com falhas e Olá número de falhas para cada VM.</span><span class="sxs-lookup"><span data-stu-id="bf51f-111">This opens hello blade **Endpoint Protection failure** which lists VMs with failures and hello number of failures for each VM.</span></span> <span data-ttu-id="bf51f-112">Selecione uma VM na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf51f-112">Select a VM from hello list.</span></span>
   <span data-ttu-id="bf51f-113">![Endpoint protection failure][2]</span><span class="sxs-lookup"><span data-stu-id="bf51f-113">![Endpoint protection failure][2]</span></span>
3. <span data-ttu-id="bf51f-114">Um **falhas lista** folha abre Olá selecionada de VM, exibindo uma lista de falhas.</span><span class="sxs-lookup"><span data-stu-id="bf51f-114">A **Failures List** blade opens for hello selected VM, displaying a list of failures.</span></span> <span data-ttu-id="bf51f-115">Selecione uma falha de saudação lista toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="bf51f-115">Select a failure from hello list toolearn more.</span></span> <span data-ttu-id="bf51f-116">Isso abrirá uma folha com informações sobre a falha de saudação selecionada.</span><span class="sxs-lookup"><span data-stu-id="bf51f-116">This opens a blade with information about hello selected failure.</span></span>
   <span data-ttu-id="bf51f-117">![Lista de falhas][3]
   ![Eventos de falha][4]</span><span class="sxs-lookup"><span data-stu-id="bf51f-117">![Failures list][3]
![Failure event][4]</span></span>

## <a name="see-also"></a><span data-ttu-id="bf51f-118">Consulte também</span><span class="sxs-lookup"><span data-stu-id="bf51f-118">See also</span></span>
<span data-ttu-id="bf51f-119">toolearn mais sobre o Centro de segurança, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="bf51f-119">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="bf51f-120">[Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md)– Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="bf51f-120">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="bf51f-121">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf51f-121">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="bf51f-122">[Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md)– Saiba como toomonitor Olá a integridade de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf51f-122">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="bf51f-123">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md)– Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="bf51f-123">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="bf51f-124">[Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="bf51f-124">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="bf51f-125">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md)– localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf51f-125">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="bf51f-126">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/)– obter notícias mais recentes de segurança do Azure hello e informações.</span><span class="sxs-lookup"><span data-stu-id="bf51f-126">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
