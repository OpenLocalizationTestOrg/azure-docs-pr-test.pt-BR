---
title: "alertas de segurança aaaHandling na Central de segurança do Azure | Microsoft Docs"
description: "Este documento ajudará a incidentes de segurança de toohandle de recursos do toouse Central de segurança do Azure."
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
ms.openlocfilehash: edb911c298a2ce93cd0ea5b22ce002005040090f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="handling-security-incidents-in-azure-security-center"></a><span data-ttu-id="8611f-103">Manipulação de Incidentes de Segurança na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="8611f-103">Handling Security Incidents in Azure Security Center</span></span>
<span data-ttu-id="8611f-104">Separação e investigando os alertas de segurança podem levar muito tempo para que os analistas de segurança mais capacitados Olá mesmo e para muitos é tooeven difícil saber onde toobegin.</span><span class="sxs-lookup"><span data-stu-id="8611f-104">Triaging and investigating security alerts can be time consuming for even hello most skilled security analysts, and for many it is hard tooeven know where toobegin.</span></span> <span data-ttu-id="8611f-105">Usando [análise](security-center-detection-capabilities.md) tooconnect informações de saudação entre distintos [alertas de segurança](security-center-managing-and-responding-alerts.md), Central de segurança pode fornecer uma única exibição de uma campanha de ataque e todos Olá relacionados alertas – você pode Compreenda rapidamente o invasor de saudação ações levou e os recursos que foram afetados.</span><span class="sxs-lookup"><span data-stu-id="8611f-105">By using [analytics](security-center-detection-capabilities.md) tooconnect hello information between distinct [security alerts](security-center-managing-and-responding-alerts.md), Security Center can provide you with a single view of an attack campaign and all of hello related alerts – you can quickly understand what actions hello attacker took and what resources were impacted.</span></span>

<span data-ttu-id="8611f-106">Este documento aborda como toouse alerta de segurança do recurso na Central de segurança tooassist você lidar com incidentes de segurança.</span><span class="sxs-lookup"><span data-stu-id="8611f-106">This document discusses how toouse security alert capability in Security Center tooassist you handling security incidents.</span></span>

## <a name="what-is-a-security-incident"></a><span data-ttu-id="8611f-107">O que é um incidente de segurança?</span><span class="sxs-lookup"><span data-stu-id="8611f-107">What is a security incident?</span></span>
<span data-ttu-id="8611f-108">Na Central de Segurança, um incidente de segurança é uma agregação de todos os alertas de um recurso que se alinham com os padrões da [cadeia de desativações](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) .</span><span class="sxs-lookup"><span data-stu-id="8611f-108">In Security Center, a security incident is an aggregation of all alerts for a resource that align with [kill chain](https://blogs.technet.microsoft.com/office365security/addressing-your-cxos-top-five-cloud-security-concerns/) patterns.</span></span> <span data-ttu-id="8611f-109">Incidentes aparecem na Olá [alertas de segurança](security-center-managing-and-responding-alerts.md) lado a lado e folha.</span><span class="sxs-lookup"><span data-stu-id="8611f-109">Incidents appear in hello [Security Alerts](security-center-managing-and-responding-alerts.md) tile and blade.</span></span> <span data-ttu-id="8611f-110">Um incidente revelará a lista de saudação de alertas relacionados, que permite que você tooobtain obter mais informações sobre cada ocorrência.</span><span class="sxs-lookup"><span data-stu-id="8611f-110">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span>

## <a name="managing-security-incidents"></a><span data-ttu-id="8611f-111">Gerenciamento de incidentes de segurança</span><span class="sxs-lookup"><span data-stu-id="8611f-111">Managing security incidents</span></span>
<span data-ttu-id="8611f-112">Você pode examinar seus incidentes de segurança atual examinando Olá bloco de alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="8611f-112">You can review your current security incidents by looking at hello security alerts tile.</span></span> <span data-ttu-id="8611f-113">Acesso Olá Portal do Azure e siga as etapas de saudação abaixo toosee mais detalhes sobre cada incidente de segurança:</span><span class="sxs-lookup"><span data-stu-id="8611f-113">Access hello Azure Portal and follow hello steps below toosee more details about each security incident:</span></span>

1. <span data-ttu-id="8611f-114">No painel de Central de segurança hello, você verá Olá **alertas de segurança** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="8611f-114">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![Bloco Alertas de segurança na Central de Segurança](./media/security-center-incident/security-center-incident-fig1.png)

2. <span data-ttu-id="8611f-116">Clique em tooexpand esse bloco-lo e se um incidente de segurança é detectado, ele será exibido no gráfico de alertas de segurança Olá conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="8611f-116">Click on this tile tooexpand it and if a security incident is detected, it will appear under hello security alerts graph as shown  below:</span></span>

    ![Incidente de segurança](./media/security-center-incident/security-center-incident-fig2.png)

3. <span data-ttu-id="8611f-118">Observe que a descrição do incidente de segurança Olá tem um ícone diferente em comparação com tooother alertas.</span><span class="sxs-lookup"><span data-stu-id="8611f-118">Notice that hello security incident description has a different icon compared tooother alerts.</span></span> <span data-ttu-id="8611f-119">Clique nela tooview mais detalhes sobre este incidente.</span><span class="sxs-lookup"><span data-stu-id="8611f-119">Click on it tooview more details about this incident.</span></span>

    ![Incidente de segurança](./media/security-center-incident/security-center-incident-fig3.png)

4. <span data-ttu-id="8611f-121">Em Olá **incidente** folha, você verá mais detalhes sobre este incidente de segurança, que inclui a descrição completa, sua severidade (que nesse caso é alta), seu estado atual (nesse caso ele ainda é *ativo*, o que implica que o usuário Olá não tiver feito tooit uma ação - isso pode ser feito pelo clique com o botão direito no incidente Olá no hello **alertas de segurança** folha), Olá atacados recurso (neste caso *VM1*), Olá etapas de correção de incidente hello e no painel inferior de saudação você tem alertas de saudação que foram incluídos neste incidente.</span><span class="sxs-lookup"><span data-stu-id="8611f-121">On hello **incident** blade you will see more details about this security incident, which includes its full description, its severity (which in this case is high), its current state (in this case it is still *active*, which implies hello user hasn't taken an action tooit - this can be done by right clicking on hello incident in hello **Security alerts** blade), hello attacked resource (in this case *VM1*), hello remediation steps for hello incident, and in hello bottom pane you have hello alerts that were included in this incident.</span></span> <span data-ttu-id="8611f-122">Se você quiser obter mais informações sobre cada alerta tooobtain, basta clicar nele e outra folha será aberta, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="8611f-122">If you want tooobtain more information on each alert, just click on it and another blade will open, as shown below:</span></span>

    ![Incidente de segurança](./media/security-center-incident/security-center-incident-fig4.png)

<span data-ttu-id="8611f-124">informações de saudação nesta folha variam de alerta de toohello de acordo.</span><span class="sxs-lookup"><span data-stu-id="8611f-124">hello information on this blade will vary according toohello alert.</span></span> <span data-ttu-id="8611f-125">Leitura [toosecurity está respondendo e gerenciamento de alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) para obter mais informações sobre como toomanage esses alertas.</span><span class="sxs-lookup"><span data-stu-id="8611f-125">Read [Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) for more information on how toomanage these alerts.</span></span> <span data-ttu-id="8611f-126">Algumas considerações importantes sobre esse recurso:</span><span class="sxs-lookup"><span data-stu-id="8611f-126">Some important considerations regarding this capability:</span></span>

* <span data-ttu-id="8611f-127">Um novo filtro permite que você toocustomize que tooincident sua exibição alertas somente, apenas, ou ambos.</span><span class="sxs-lookup"><span data-stu-id="8611f-127">A new filter enables you toocustomize your view tooIncident only, Alerts only, or both.</span></span>
* <span data-ttu-id="8611f-128">Olá mesmo alerta pode existir como parte de um incidente (se aplicável), bem como toobe visível como um alerta autônomo.</span><span class="sxs-lookup"><span data-stu-id="8611f-128">hello same alert can exist as part of an Incident (if applicable), as well as toobe visible as a standalone alert.</span></span>

## <a name="see-also"></a><span data-ttu-id="8611f-129">Consulte também</span><span class="sxs-lookup"><span data-stu-id="8611f-129">See also</span></span>
<span data-ttu-id="8611f-130">Neste documento, você aprendeu como toouse Olá do recurso incidente de segurança na Central de segurança.</span><span class="sxs-lookup"><span data-stu-id="8611f-130">In this document, you learned how toouse hello security incident capability in Security Center.</span></span> <span data-ttu-id="8611f-131">toolearn mais sobre o Centro de segurança, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="8611f-131">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="8611f-132">Gerenciando e responder a alertas toosecurity na Central de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="8611f-132">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* [<span data-ttu-id="8611f-133">Recursos de detecção da Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="8611f-133">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="8611f-134">Guia de planejamento e operações da Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="8611f-134">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* [<span data-ttu-id="8611f-135">Gerenciando e responder a alertas toosecurity na Central de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="8611f-135">Managing and responding toosecurity alerts in Azure Security Center</span></span>](security-center-managing-and-responding-alerts.md)
* <span data-ttu-id="8611f-136">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md)– localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="8611f-136">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="8611f-137">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/): encontre postagens no blog sobre a conformidade e a segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="8611f-137">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Find blog posts about Azure security and compliance.</span></span>
