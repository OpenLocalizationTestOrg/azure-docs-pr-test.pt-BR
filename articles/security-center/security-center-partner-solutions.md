---
title: "soluções de parceiros de aaaManaging na Central de segurança do Azure | Microsoft Docs"
description: "Este documento orienta a como a Central de segurança do Azure permite que você monitor com um status de integridade de saudação rapidamente suas soluções de parceiros integrados com sua assinatura do Azure."
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
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a><span data-ttu-id="1267f-103">Monitoramento de soluções de parceiros com a Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="1267f-103">Monitoring partner solutions with Azure Security Center</span></span>
<span data-ttu-id="1267f-104">Este documento o orienta como toomonitor Olá status de integridade de suas soluções de parceiros na Central de segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="1267f-104">This document walks you through how toomonitor hello health status of your partner solutions in Azure Security Center.</span></span>

> [!NOTE]
> <span data-ttu-id="1267f-105">Este documento apresenta serviço hello usando um exemplo de implantação.</span><span class="sxs-lookup"><span data-stu-id="1267f-105">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="1267f-106">Este documento não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="1267f-106">This document is not a step-by-step guide.</span></span>
>
>

## <a name="monitoring-partner-solutions"></a><span data-ttu-id="1267f-107">Monitoramento das soluções de parceiros</span><span class="sxs-lookup"><span data-stu-id="1267f-107">Monitoring partner solutions</span></span>
<span data-ttu-id="1267f-108">Olá **soluções de parceiros** bloco Olá **Central de segurança** permite folha monitorar em um status de integridade de saudação rapidamente suas soluções de parceiros que estão integradas com sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="1267f-108">hello **Partner solutions** tile on hello **Security Center** blade lets you monitor at a glance hello health status of your partner solutions that are integrated with your Azure subscription.</span></span>

![Bloco Soluções de parceiros][1]

<span data-ttu-id="1267f-110">Olá **soluções de parceiros** lado a lado exibe o saudação várias soluções de parceiros integrados com sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="1267f-110">hello **Partner solutions** tile displays hello number of partner solutions integrated with your subscription.</span></span> <span data-ttu-id="1267f-111">Se não houver nenhum soluções integradas, o bloco Olá exibe o número de Olá zero.</span><span class="sxs-lookup"><span data-stu-id="1267f-111">If there are no solutions integrated, hello tile displays hello number zero.</span></span>

<span data-ttu-id="1267f-112">integridade de saudação tooview suas soluções de parceiros:</span><span class="sxs-lookup"><span data-stu-id="1267f-112">tooview hello health of your partner solutions:</span></span>

1. <span data-ttu-id="1267f-113">Selecione Olá **soluções de parceiros** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="1267f-113">Select hello **Partner solutions** tile.</span></span> <span data-ttu-id="1267f-114">Olá **soluções de parceiros** folha abre exibindo uma lista de suas soluções de parceiro conectado tooSecurity Center.</span><span class="sxs-lookup"><span data-stu-id="1267f-114">hello **Partner solutions** blade opens displaying a list of your partner solutions connected tooSecurity Center.</span></span>

   ![Soluções de parceiros][3]

   <span data-ttu-id="1267f-116">saudação status de uma solução de parceiro pode ser:</span><span class="sxs-lookup"><span data-stu-id="1267f-116">hello status of a partner solution can be:</span></span>

   * <span data-ttu-id="1267f-117">Protegido (verde) - não há qualquer problema de integridade</span><span class="sxs-lookup"><span data-stu-id="1267f-117">Protected (green) - there is no health issue.</span></span>
   * <span data-ttu-id="1267f-118">Não íntegro (vermelho) - há um problema de integridade que requer atenção imediata</span><span class="sxs-lookup"><span data-stu-id="1267f-118">Unhealthy (red) - there is a health issue that requires immediate attention.</span></span>
   * <span data-ttu-id="1267f-119">Parado reporting (laranja) - solução Olá parou a relatar sua integridade.</span><span class="sxs-lookup"><span data-stu-id="1267f-119">Stopped reporting (orange) - hello solution has stopped reporting its health.</span></span>
   * <span data-ttu-id="1267f-120">Status da proteção desconhecido (laranja) - integridade Olá de solução de saudação é desconhecido no momento devido tooa falhado o processo de adição de uma nova solução existente de toohello de recursos.</span><span class="sxs-lookup"><span data-stu-id="1267f-120">Unknown protection status (orange) - hello health of hello solution is unknown at this time due tooa failed process of adding a new resource toohello existing solution.</span></span>
   * <span data-ttu-id="1267f-121">Não relatar (cinza) - solução de saudação não relatou qualquer coisa ainda, status de uma solução pode ser não relatados se recentemente foi conectado e ainda está sendo implantado.</span><span class="sxs-lookup"><span data-stu-id="1267f-121">Not reported (gray) - hello solution has not reported anything yet, a solution's status may be unreported if it has recently been connected and is still deploying.</span></span>

2. <span data-ttu-id="1267f-122">Selecione uma solução de parceiro.</span><span class="sxs-lookup"><span data-stu-id="1267f-122">Select a partner solution.</span></span> <span data-ttu-id="1267f-123">Neste exemplo, permite que selecione Olá **Qualys** solução.</span><span class="sxs-lookup"><span data-stu-id="1267f-123">In this example, lets select hello **Qualys** solution.</span></span>  <span data-ttu-id="1267f-124">Uma folha abre mostrando recursos associados do status de saudação de solução de parceiro de saudação e solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="1267f-124">A blade opens showing you hello status of hello partner solution and hello solution's associated resources.</span></span> <span data-ttu-id="1267f-125">Selecione **console de solução** experiência de gerenciamento de parceiros de saudação tooopen para esta solução.</span><span class="sxs-lookup"><span data-stu-id="1267f-125">Select **Solution console** tooopen hello partner management experience for this solution.</span></span>

   ![Detalhes da solução de parceiro][4]
3. <span data-ttu-id="1267f-127">Voltar toohello **Qualys** folha e selecione **Link VM**.</span><span class="sxs-lookup"><span data-stu-id="1267f-127">Go back toohello **Qualys** blade and select **Link VM**.</span></span> <span data-ttu-id="1267f-128">Olá **aplicativos de Link** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="1267f-128">hello **Link Applications** blade opens.</span></span> <span data-ttu-id="1267f-129">Aqui você pode conectar a solução de parceiro de toohello de recursos.</span><span class="sxs-lookup"><span data-stu-id="1267f-129">Here you can connect resources toohello partner solution.</span></span>

   ![Solução de toopartner de recursos do link][5]

## <a name="next-steps"></a><span data-ttu-id="1267f-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1267f-131">Next steps</span></span>
<span data-ttu-id="1267f-132">Neste documento, você foram introduzida toohello **soluções de parceiros** lado a lado na Central de segurança.</span><span class="sxs-lookup"><span data-stu-id="1267f-132">In this document, you were introduced toohello **Partner Solutions** tile in Security Center.</span></span> <span data-ttu-id="1267f-133">toolearn mais sobre o Centro de segurança, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1267f-133">toolearn more about Security Center, see hello following articles:</span></span>

* <span data-ttu-id="1267f-134">[Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) — Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="1267f-134">[Setting security policies in Azure Security Center](security-center-policies.md) — Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="1267f-135">[Gerenciando as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1267f-135">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) — Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="1267f-136">[Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) — Saiba como toomonitor Olá a integridade de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1267f-136">[Security health monitoring in Azure Security Center](security-center-monitoring.md) — Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="1267f-137">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) — Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="1267f-137">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) — Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="1267f-138">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="1267f-138">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="1267f-139">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) — Obtenha notícias mais recentes de segurança do Azure hello e informações.</span><span class="sxs-lookup"><span data-stu-id="1267f-139">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
