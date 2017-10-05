---
title: "Gerenciamento de soluções de parceiros na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento fornece uma orientação de como a Central de Segurança do Azure permite que você monitore rapidamente o status de integridade de suas soluções de parceiro integradas com sua assinatura do Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: 2ebb930e877c5027f4d7b0a316a7f5ebe84471b1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="c50ad-103">Monitoramento de soluções de parceiros com a Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="c50ad-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="c50ad-104">Este documento orienta sobre como monitorar o status de integridade de suas soluções de parceiro na Central de Segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="c50ad-104">This document walks you through how to monitor the health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="c50ad-105">Este documento apresenta o serviço usando uma implantação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c50ad-105">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="c50ad-106">Este documento não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="c50ad-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="c50ad-107">Monitoramento das soluções de parceiros</span><span class="sxs-lookup"><span data-stu-id="c50ad-107">Monitoring partner solutions</span></span>
<span data-ttu-id="c50ad-108">O bloco **Soluções de parceiros** na folha **Central de Segurança** permite que você monitore rapidamente o status de integridade de suas soluções de parceiro integradas com sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c50ad-108">The **Partner solutions** tile on the **Security Center** blade lets you monitor at a glance the health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![Bloco Soluções de parceiros][1]

<span data-ttu-id="c50ad-110">O bloco **Soluções de parceiros** exibe o número de soluções de parceiros integradas à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c50ad-110">The **Partner solutions** tile displays the number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="c50ad-111">Se não houver nenhuma solução integrada, o bloco exibirá o número zero.</span><span class="sxs-lookup"><span data-stu-id="c50ad-111">If there are no solutions integrated, the tile displays the number zero.</span></span>

<span data-ttu-id="c50ad-112">Para exibir a integridade das soluções de seu parceiro:</span><span class="sxs-lookup"><span data-stu-id="c50ad-112">To view the health of your partner solutions:</span></span>

1. <span data-ttu-id="c50ad-113">Selecione o bloco **Soluções de parceiros** .</span><span class="sxs-lookup"><span data-stu-id="c50ad-113">Select the **Partner solutions** tile.</span></span> <span data-ttu-id="c50ad-114">A folha **Soluções de parceiros** será aberta, exibindo uma lista das soluções de parceiros conectadas à Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="c50ad-114">The **Partner solutions** blade opens displaying a list of your partner solutions connected to Security Center.</span></span>

   ![Soluções de parceiros][3]

   <span data-ttu-id="c50ad-116">O status de uma solução de parceiro pode ser:</span><span class="sxs-lookup"><span data-stu-id="c50ad-116">The status of a partner solution can be:</span></span>

   * <span data-ttu-id="c50ad-117">Protegido (verde) - não há qualquer problema de integridade</span><span class="sxs-lookup"><span data-stu-id="c50ad-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="c50ad-118">Não íntegro (vermelho) - há um problema de integridade que requer atenção imediata</span><span class="sxs-lookup"><span data-stu-id="c50ad-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="c50ad-119">Parou de relatar (laranja) - a solução interrompeu o envio de relatórios sobre sua integridade</span><span class="sxs-lookup"><span data-stu-id="c50ad-119">Stopped reporting (orange) - the solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="c50ad-120">Status de proteção desconhecido (laranja) - a integridade da solução é desconhecida no momento devido a um processo para adicionar um novo recurso à solução existente com falha.</span><span class="sxs-lookup"><span data-stu-id="c50ad-120">Unknown protection status (orange) - the health of the solution is unknown at this time due to a failed process of adding a new resource to the existing solution.</span></span>
   * <span data-ttu-id="c50ad-121">Não relatado (cinza) - a solução não reportou nada ainda. O status da solução pode não ser relatado se tiver sido conectada recentemente e ainda estiver sendo implantada.</span><span class="sxs-lookup"><span data-stu-id="c50ad-121">Not reported (gray) - the solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="c50ad-122">Selecione uma solução de parceiro.</span><span class="sxs-lookup"><span data-stu-id="c50ad-122">Select a partner solution.</span></span> <span data-ttu-id="c50ad-123">Neste exemplo, vamos selecionar a solução **Qualys**.</span><span class="sxs-lookup"><span data-stu-id="c50ad-123">In this example, lets select the **Qualys** solution.</span></span>  <span data-ttu-id="c50ad-124">Uma folha será aberta mostrando o status da solução de parceiro e dos recursos associados a ela.</span><span class="sxs-lookup"><span data-stu-id="c50ad-124">A blade opens showing you the status of the partner solution and the solution's associated resources.</span></span> <span data-ttu-id="c50ad-125">Selecione **Console da solução** para abrir a experiência de gerenciamento do parceiro para essa solução.</span><span class="sxs-lookup"><span data-stu-id="c50ad-125">Select **Solution console** to open the partner management experience for this solution.</span></span>

   ![Detalhes da solução de parceiro][4]
3. <span data-ttu-id="c50ad-127">Retorne à folha **Qualys** e selecione **Vincular VM**.</span><span class="sxs-lookup"><span data-stu-id="c50ad-127">Go back to the **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="c50ad-128">A folha **Vincular Aplicativos** é aberta.</span><span class="sxs-lookup"><span data-stu-id="c50ad-128">The **Link Applications** blade opens.</span></span> <span data-ttu-id="c50ad-129">Nela, você pode conectar recursos à solução de parceiro.</span><span class="sxs-lookup"><span data-stu-id="c50ad-129">Here you can connect resources to the partner solution.</span></span>

   ![Vincular recursos à solução de parceiro][5]

## <a name="next-steps"></a><span data-ttu-id="c50ad-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c50ad-131">Next steps</span></span>
<span data-ttu-id="c50ad-132">Neste documento, você foi apresentado às **Soluções de Parceiros** na Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="c50ad-132">In this document, you were introduced to the **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="c50ad-133">Para saber mais sobre a Central de Segurança, confira estes artigos:</span><span class="sxs-lookup"><span data-stu-id="c50ad-133">To learn more about Security Center, see the following articles:</span></span>

* <span data-ttu-id="c50ad-134">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md) : saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c50ad-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="c50ad-135">[Gerenciando as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c50ad-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c50ad-136">[Monitoramento da integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md) : saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c50ad-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="c50ad-137">[Gerenciando e respondendo aos alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) : aprenda a gerenciar e responder aos alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="c50ad-137">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="c50ad-138">[Perguntas frequentes da Central de Segurança do Azure](security-center-faq.md) : encontre as perguntas frequentes sobre como usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="c50ad-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="c50ad-139">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) : obtenha as últimas notícias de segurança e informações do Azure.</span><span class="sxs-lookup"><span data-stu-id="c50ad-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
