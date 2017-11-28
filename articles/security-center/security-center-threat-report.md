---
title: "Relatório de inteligência de ameaças da Central de Segurança do Azure | Microsoft Docs"
description: "Este documento ajuda a usar os Relatórios de Inteligência de Ameaças da Central de Segurança do Azure durante uma investigação para obter mais informações sobre um alerta de segurança."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5662e312-e8c2-4736-974e-576eeb333484
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: b4310cf4e6849c67031b3ec8b1fd5957e35f7ea6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a><span data-ttu-id="fd095-103">Relatório de Inteligência de Ameaças da Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="fd095-103">Azure Security Center Threat Intelligence Report</span></span>
<span data-ttu-id="fd095-104">Este documento explica como os Relatórios Inteligentes de Ameças da Central de Segurança do Azure podem ajudá-lo a saber mais sobre uma ameaça que gerou um alerta de segurança.</span><span class="sxs-lookup"><span data-stu-id="fd095-104">This document explains how Azure Security Center Threat Intelligent Reports can help you learn more about a threat that generated a security alert.</span></span>

## <a name="what-is-a-threat-intelligence-report"></a><span data-ttu-id="fd095-105">O que é um relatório de inteligência de ameaças?</span><span class="sxs-lookup"><span data-stu-id="fd095-105">What is a threat intelligence report?</span></span>
<span data-ttu-id="fd095-106">A detecção de ameaças da Central de Segurança funciona monitorando informações de segurança de seus recursos do Azure, de rede e de soluções de parceiros conectados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fd095-106">Security Center threat detection works by monitoring security information from your Azure resources, the network, and connected partner solutions.</span></span> <span data-ttu-id="fd095-107">Ele analisa essas informações geralmente correlacionando informações de várias fontes para identificar ameaças.</span><span class="sxs-lookup"><span data-stu-id="fd095-107">It analyzes this information, often correlating information from multiple sources, to identify threats.</span></span> <span data-ttu-id="fd095-108">Esse processo faz parte dos [recursos de detecção](security-center-detection-capabilities.md) da Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="fd095-108">This process is part of the Security Center [detection capabilities](security-center-detection-capabilities.md).</span></span>

<span data-ttu-id="fd095-109">Quando a Central de Segurança identifica uma ameaça, ele dispara um [alerta de segurança](security-center-managing-and-responding-alerts.md), que contém informações sobre um evento específico, incluindo sugestões de correção detalhadas.</span><span class="sxs-lookup"><span data-stu-id="fd095-109">When Security Center identifies a threat, it will trigger a [security alert](security-center-managing-and-responding-alerts.md), which contains detailed information regarding a particular event, including suggestions for remediation.</span></span> <span data-ttu-id="fd095-110">Para ajudar as equipes de resposta a incidentes a investigar e a corrigir ameaças, a Central de Segurança inclui um relatório de inteligência de ameaças que contém informações sobre a ameaça detectada, incluindo informações como :</span><span class="sxs-lookup"><span data-stu-id="fd095-110">To assist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about the threat that was detected, including information such as the:</span></span>

* <span data-ttu-id="fd095-111">Identidade ou associações do invasor (se essas informações estiverem disponíveis)</span><span class="sxs-lookup"><span data-stu-id="fd095-111">Attacker’s identity or associations (if this information is available)</span></span>
* <span data-ttu-id="fd095-112">Objetivos dos invasores</span><span class="sxs-lookup"><span data-stu-id="fd095-112">Attackers’ objectives</span></span>
* <span data-ttu-id="fd095-113">Campanhas de ataque atuais e históricas (se essas informações estiverem disponíveis)</span><span class="sxs-lookup"><span data-stu-id="fd095-113">Current and historical attack campaigns (if this information is available)</span></span>
* <span data-ttu-id="fd095-114">Táticas, ferramentas e procedimentos dos invasores</span><span class="sxs-lookup"><span data-stu-id="fd095-114">Attackers’ tactics, tools and procedures</span></span>
* <span data-ttu-id="fd095-115">Indicadores associados de comprometimento (IoC), como URLs e hashes de arquivo</span><span class="sxs-lookup"><span data-stu-id="fd095-115">Associated indicators of compromise (IoC) such as URLs and file hashes</span></span>
* <span data-ttu-id="fd095-116">Vitimologia, que é a prevalência do setor e geográfica para auxiliar você na determinação se seus recursos do Azure estão em risco</span><span class="sxs-lookup"><span data-stu-id="fd095-116">Victimology, which is the industry and geographic prevalence to assist you in determining if your Azure resources are at risk</span></span>
* <span data-ttu-id="fd095-117">Informações de atenuação e correção</span><span class="sxs-lookup"><span data-stu-id="fd095-117">Mitigation and remediation information</span></span>

> [!NOTE]
> <span data-ttu-id="fd095-118">A quantidade de informações em qualquer relatório específico varia; o nível de detalhes baseia-se na atividade e na prevalência do malware.</span><span class="sxs-lookup"><span data-stu-id="fd095-118">The amount of information in any particular report will vary; the level of detail is based on the malware’s activity and prevalence.</span></span>
>
>

<span data-ttu-id="fd095-119">A Central de Segurança tem três tipos de relatórios de ameaça, que podem variar de acordo com o ataque.</span><span class="sxs-lookup"><span data-stu-id="fd095-119">Security Center has three types of threat reports, which can vary according to the attack.</span></span> <span data-ttu-id="fd095-120">Os relatórios disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="fd095-120">The reports available are:</span></span>

* <span data-ttu-id="fd095-121">**Relatório de Grupo de Atividades**: fornece análises avançadas sobre os invasores, seus objetivos e táticas.</span><span class="sxs-lookup"><span data-stu-id="fd095-121">**Activity Group Report**: provides deep dives into attackers, their objectives and tactics.</span></span>
* <span data-ttu-id="fd095-122">**Relatório de Campanha**: concentra-se nos detalhes de campanhas de ataque específicas.</span><span class="sxs-lookup"><span data-stu-id="fd095-122">**Campaign Report**: focuses on details of specific attack campaigns.</span></span>
* <span data-ttu-id="fd095-123">**Relatório de Resumo de Ameaças**: abrange todos os itens dos dois relatórios anteriores.</span><span class="sxs-lookup"><span data-stu-id="fd095-123">**Threat Summary Report**: covers all of the items in the previous two reports.</span></span>

<span data-ttu-id="fd095-124">Esse tipo de informação é muito útil durante o processo de [resposta a incidentes](security-center-incident-response.md), onde há uma investigação em andamento para compreender a origem do ataque, as motivações do invasor e o que fazer para atenuar esse problema no futuro.</span><span class="sxs-lookup"><span data-stu-id="fd095-124">This type of information is very useful during the [incident response](security-center-incident-response.md) process, where there is an ongoing investigation to understand the source of the attack, the attacker’s motivations, and what to do to mitigate this issue moving forward.</span></span>

## <a name="how-to-access-the-threat-intelligence-report"></a><span data-ttu-id="fd095-125">Como acessar o relatório de inteligência de ameaças?</span><span class="sxs-lookup"><span data-stu-id="fd095-125">How to access the threat intelligence report?</span></span>
<span data-ttu-id="fd095-126">Você pode examinar os alertas atuais observando o bloco **Alertas de segurança** .</span><span class="sxs-lookup"><span data-stu-id="fd095-126">You can review your current alerts by looking at the **Security alerts** tile.</span></span> <span data-ttu-id="fd095-127">Abra o Portal do Azure e siga as etapas abaixo para ver mais detalhes sobre cada alerta:</span><span class="sxs-lookup"><span data-stu-id="fd095-127">Open the Azure Portal and follow the steps below to see more details about each alert:</span></span>

1. <span data-ttu-id="fd095-128">No painel Central de Segurança, você verá o bloco **Alertas de segurança** .</span><span class="sxs-lookup"><span data-stu-id="fd095-128">On the Security Center dashboard, you will see the **Security alerts** tile.</span></span>
2. <span data-ttu-id="fd095-129">Clique no bloco para abrir a folha **Alertas de segurança** que contém mais detalhes sobre os alertas e clique no alerta de segurança sobre o qual você deseja obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="fd095-129">Click the tile to open the **Security alerts** blade that contains more details about the alerts and click in the security alert that you want to obtain more information about.</span></span>

    ![Alertas de segurança](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. <span data-ttu-id="fd095-131">Nesse caso, a folha **Processo suspeito executado** mostra os detalhes sobre o alerta, conforme mostrado na figura a seguir:</span><span class="sxs-lookup"><span data-stu-id="fd095-131">In this case the **Suspicious process executed** blade shows the details about the alert as shown in the figure below:</span></span>

    ![Detalhes do alerta de segurança](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. <span data-ttu-id="fd095-133">A quantidade de informações disponíveis para cada alerta de segurança varia de acordo com o tipo de alerta.</span><span class="sxs-lookup"><span data-stu-id="fd095-133">The amount of information available for each security alert will vary according to the type of alert.</span></span> <span data-ttu-id="fd095-134">No campo **RELATÓRIOS**, você tem um link para o relatório de inteligência de ameaça.</span><span class="sxs-lookup"><span data-stu-id="fd095-134">In the **REPORTS** field you have a link to the threat intelligence report.</span></span> <span data-ttu-id="fd095-135">Clique nele e outra janela do navegador será exibida com o arquivo PDF.</span><span class="sxs-lookup"><span data-stu-id="fd095-135">Click on it and another browser window will appear with PDF file.</span></span>

   ![Seleção de armazenamento](./media/security-center-threat-report/security-center-threat-report-fig3.png)

<span data-ttu-id="fd095-137">Aqui você pode baixar o PDF para esse relatório e ler mais sobre o problema de segurança detectado e executar ações com base nas informações fornecidas.</span><span class="sxs-lookup"><span data-stu-id="fd095-137">From here you can download the PDF for this report and read more about the security issue that was detected and take actions based on the information provided.</span></span>

## <a name="see-also"></a><span data-ttu-id="fd095-138">Consulte também</span><span class="sxs-lookup"><span data-stu-id="fd095-138">See also</span></span>
<span data-ttu-id="fd095-139">Neste documento, você aprendeu como os Relatórios de Inteligência de Ameaças da Central de Segurança do Azure podem ajudar durante uma investigação sobre alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="fd095-139">In this document, you learned how Azure Security Center Threat Intelligent Reports can help during an investigation about security alerts.</span></span> <span data-ttu-id="fd095-140">Para saber mais sobre a Central de Segurança do Azure, veja o seguinte:</span><span class="sxs-lookup"><span data-stu-id="fd095-140">To learn more about Azure Security Center, see the following:</span></span>

* <span data-ttu-id="fd095-141">[Perguntas Frequentes sobre a Central de Segurança do Azure](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="fd095-141">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="fd095-142">Encontre as perguntas frequentes sobre como usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="fd095-142">Find frequently asked questions about using the service.</span></span>
* [<span data-ttu-id="fd095-143">Aproveitando a Central de Segurança do Azure para a resposta a incidentes</span><span class="sxs-lookup"><span data-stu-id="fd095-143">Leveraging Azure Security Center for Incident Response</span></span>](security-center-incident-response.md)
* [<span data-ttu-id="fd095-144">Recursos de detecção da Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="fd095-144">Azure Security Center detection capabilities</span></span>](security-center-detection-capabilities.md)
* <span data-ttu-id="fd095-145">[Guia de planejamento e operações da Central de Segurança do Azure](security-center-planning-and-operations-guide.md).</span><span class="sxs-lookup"><span data-stu-id="fd095-145">[Azure Security Center planning and operations guide](security-center-planning-and-operations-guide.md).</span></span> <span data-ttu-id="fd095-146">Saiba como planejar e entender as considerações de design para adotar a Central de Segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd095-146">Learn how to plan and understand the design considerations to adopt Azure Security Center.</span></span>
* <span data-ttu-id="fd095-147">[Gerenciando e respondendo aos alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="fd095-147">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md).</span></span> <span data-ttu-id="fd095-148">Saiba como gerenciar e responder aos alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="fd095-148">Learn how to manage and respond to security alerts.</span></span>
* [<span data-ttu-id="fd095-149">Manipulação de incidente de segurança na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="fd095-149">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* <span data-ttu-id="fd095-150">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="fd095-150">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="fd095-151">Encontre postagens no blog sobre a conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd095-151">Find blog posts about Azure security and compliance.</span></span>
