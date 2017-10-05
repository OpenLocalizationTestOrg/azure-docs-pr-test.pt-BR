---
title: "Gerenciamento de alertas de segurança na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento ajuda você a usar os recursos da Central de Segurança do Azure para gerenciar incidentes de segurança."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: e8feb669-8f30-49eb-ba38-046edf3f9656
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: a302f8cb2555eef469a24da2523fdd9b97cc5730
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a><span data-ttu-id="bf003-103">Manipulação de Incidentes de Segurança na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="bf003-103">Handling Security Incidents in Azure Security Center</span></span>
<span data-ttu-id="bf003-104">A triagem e investigação de alertas de segurança pode ser uma tarefa demorada até mesmo para os analistas de segurança mais capacitados, e, para muitos, é difícil até mesmo saber por onde começar.</span><span class="sxs-lookup"><span data-stu-id="bf003-104">Triaging and investigating security alerts can be time consuming for even the most skilled security analysts, and for many it is hard to even know where to begin.</span></span> <span data-ttu-id="bf003-105">Usando [análise](security-center-detection-capabilities.md) para conectar as informações entre diferentes [alertas de segurança](security-center-managing-and-responding-alerts.md), a Central de Segurança pode fornecer uma exibição única de uma campanha de ataque e todos os alertas relacionados, com isso, você pode entender rapidamente quais ações o invasor executou e quais recursos foram afetados.</span><span class="sxs-lookup"><span data-stu-id="bf003-105">By using [analytics](security-center-detection-capabilities.md) to connect the information between distinct [security alerts](security-center-managing-and-responding-alerts.md), Security Center can provide you with a single view of an attack campaign and all of the related alerts – you can quickly understand what actions the attacker took and what resources were impacted.</span></span>

<span data-ttu-id="bf003-106">Este documento discute como usar o recurso de alerta de segurança na Central de Segurança para ajudar a lidar com incidentes de segurança.</span><span class="sxs-lookup"><span data-stu-id="bf003-106">This document discusses how to use security alert capability in Security Center to assist you handling security incidents.</span></span>

## <a name="what-is-a-security-incident"></a><span data-ttu-id="bf003-107">O que é um incidente de segurança?</span><span class="sxs-lookup"><span data-stu-id="bf003-107">What is a security incident?</span></span>
<span data-ttu-id="bf003-108">Na Central de Segurança, um incidente de segurança é uma agregação de todos os alertas de um recurso que se alinham com os padrões da [cadeia de desativações](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) .</span><span class="sxs-lookup"><span data-stu-id="bf003-108">In Security Center, a security incident is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span></span> <span data-ttu-id="bf003-109">Incidentes aparecem no bloco e folha [Alertas de Segurança](security-center-managing-and-responding-alerts.md) .</span><span class="sxs-lookup"><span data-stu-id="bf003-109">Incidents appear in the [Security Alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span></span> <span data-ttu-id="bf003-110">Um Incidente revelará a lista de alertas relacionados, o que permite a obtenção de mais informações sobre cada ocorrência.</span><span class="sxs-lookup"><span data-stu-id="bf003-110">An Incident will reveal the list of related alerts, which enables you to obtain more information about each occurrence.</span></span>

## <a name="managing-security-incidents"></a><span data-ttu-id="bf003-111">Gerenciamento de incidentes de segurança</span><span class="sxs-lookup"><span data-stu-id="bf003-111">Managing security incidents</span></span>
<span data-ttu-id="bf003-112">Você pode examinar os incidentes atuais de segurança observando o bloco de alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="bf003-112">You can review your current security incidents by looking at the security alerts tile.</span></span> <span data-ttu-id="bf003-113">Acesse o Portal do Azure e execute as etapas abaixo para ver mais detalhes sobre cada incidente de segurança:</span><span class="sxs-lookup"><span data-stu-id="bf003-113">Access the Azure Portal and follow the steps below to see more details about each security incident:</span></span>

1. <span data-ttu-id="bf003-114">No painel Central de Segurança, você verá o bloco **Alertas de segurança** .</span><span class="sxs-lookup"><span data-stu-id="bf003-114">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>

    ![Bloco Alertas de segurança na Central de Segurança](./media/security-center-incident/security-center-incident-fig1.png)

2. <span data-ttu-id="bf003-116">Clique nesse bloco para expandi-lo e se um incidente de segurança for detectado, ele aparecerá no gráfico de alertas de segurança, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="bf003-116">Click on this tile to expand it and if a security incident is detected, it will appear under the security alerts graph as shown  below:</span></span>

    ![Incidente de segurança](./media/security-center-incident/security-center-incident-fig2.png)

3. <span data-ttu-id="bf003-118">Observe que a descrição de incidentes de segurança tem um ícone diferente em comparação com outros alertas.</span><span class="sxs-lookup"><span data-stu-id="bf003-118">Notice that the security incident description has a different icon compared to other alerts.</span></span> <span data-ttu-id="bf003-119">Clique para exibir mais detalhes sobre o incidente.</span><span class="sxs-lookup"><span data-stu-id="bf003-119">Click on it to view more details about this incident.</span></span>

    ![Incidente de segurança](./media/security-center-incident/security-center-incident-fig3.png)

4. <span data-ttu-id="bf003-121">Na folha **incidente**, você verá mais detalhes sobre esse incidente de segurança, que inclui uma descrição completa, sua gravidade (que nesse caso é alta), estado atual (nesse caso ainda é *ativo*, o que implica que o usuário não executou uma ação para ele - isso pode ser feito clicando com o botão direito no incidente na folha **Alertas de segurança**), recurso atacado (nesse caso *VM1*), as etapas de correção do incidente e no painel inferior, você tem os alertas que foram incluídos no incidente.</span><span class="sxs-lookup"><span data-stu-id="bf003-121">On the **incident** blade you will see more details about this security incident, which includes its full description, its severity (which in this case is high), its current state (in this case it is still *active*, which implies the user hasn't taken an action to it - this can be done by right clicking on the incident in the **Security alerts** blade), the attacked resource (in this case *VM1*), the remediation steps for the incident, and in the bottom pane you have the alerts that were included in this incident.</span></span> <span data-ttu-id="bf003-122">Se você quiser obter mais informações sobre cada alerta, basta clicar nele e outra folha será aberta, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="bf003-122">If you want to obtain more information on each alert, just click on it and another blade will open, as shown below:</span></span>

    ![Incidente de segurança](./media/security-center-incident/security-center-incident-fig4.png)

<span data-ttu-id="bf003-124">As informações nessa folha variam de acordo com o alerta.</span><span class="sxs-lookup"><span data-stu-id="bf003-124">The information on this blade will vary according to the alert.</span></span> <span data-ttu-id="bf003-125">Leia [Gerenciamento e resposta aos alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) para saber mais sobre como gerenciar esses alertas.</span><span class="sxs-lookup"><span data-stu-id="bf003-125">Read [Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) for more information on how to manage these alerts.</span></span> <span data-ttu-id="bf003-126">Algumas considerações importantes sobre esse recurso:</span><span class="sxs-lookup"><span data-stu-id="bf003-126">Some important considerations regarding this capability:</span></span>

* <span data-ttu-id="bf003-127">Um novo filtro permite que você personalize para exibir para apenas Incidentes, somente Alertas ou ambos.</span><span class="sxs-lookup"><span data-stu-id="bf003-127">A new filter enables you to customize your view to Incident only, Alerts only, or both.</span></span>
* <span data-ttu-id="bf003-128">O mesmo alerta pode existir como parte de um Incidente (se aplicável), bem como para ser visível como um alerta autônomo.</span><span class="sxs-lookup"><span data-stu-id="bf003-128">The same alert can exist as part of an Incident (if applicable), as well as to be visible as a standalone alert.</span></span>

## <a name="see-also"></a><span data-ttu-id="bf003-129">Consulte também</span><span class="sxs-lookup"><span data-stu-id="bf003-129">See also</span></span>
<span data-ttu-id="bf003-130">Neste documento, você aprendeu a usar os recursos de incidente de segurança na Central de Segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf003-130">In this document, you learned how to use the security incident capability in Security Center.</span></span> <span data-ttu-id="bf003-131">Para saber mais sobre a Central de Segurança, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bf003-131">To learn more about Security Center, see the following:</span></span>

* [<span data-ttu-id="bf003-132">Gerenciando e respondendo a alertas de segurança na Central de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="bf003-132">Managing and responding to security alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="bf003-133">Recursos de detecção da Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="bf003-133">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="bf003-134">Guia de planejamento e operações da Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="bf003-134">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="bf003-135">Gerenciando e respondendo a alertas de segurança na Central de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="bf003-135">Managing and responding to security alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="bf003-136">[Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md)– encontre perguntas frequentes sobre como usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="bf003-136">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="bf003-137">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/): encontre postagens no blog sobre a conformidade e a segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf003-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Find blog posts about Azure security and compliance.</span></span>
