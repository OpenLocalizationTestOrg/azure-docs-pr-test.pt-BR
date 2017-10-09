---
title: "alertas de segurança aaaManage na Central de segurança do Azure | Microsoft Docs"
description: "Este documento ajuda você toouse Central de segurança do Azure recursos toomanage e responde a alertas de toosecurity."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a><span data-ttu-id="c507b-103">Gerenciando e responder a alertas toosecurity na Central de segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="c507b-103">Managing and responding toosecurity alerts in Azure Security Center</span></span>
<span data-ttu-id="c507b-104">Este documento ajuda você a usar a Central de segurança do Azure toomanage e responder a alertas toosecurity.</span><span class="sxs-lookup"><span data-stu-id="c507b-104">This document helps you use Azure Security Center toomanage and respond toosecurity alerts.</span></span>

> [!NOTE]
> <span data-ttu-id="c507b-105">detecções de tooenable avançado, atualização tooAzure Central de segurança padrão.</span><span class="sxs-lookup"><span data-stu-id="c507b-105">tooenable advanced detections, upgrade tooAzure Security Center Standard.</span></span> <span data-ttu-id="c507b-106">Há uma avaliação gratuita de 60 dias disponível.</span><span class="sxs-lookup"><span data-stu-id="c507b-106">A free 60-day trial is available.</span></span> <span data-ttu-id="c507b-107">tooupgrade, selecione preço no hello [política de segurança](security-center-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c507b-107">tooupgrade, select Pricing Tier in hello [Security Policy](security-center-policies.md).</span></span> <span data-ttu-id="c507b-108">Consulte [Central de segurança do Azure preços](security-center-pricing.md) toolearn mais.</span><span class="sxs-lookup"><span data-stu-id="c507b-108">See [Azure Security Center pricing](security-center-pricing.md) toolearn more.</span></span>
>
>

## <a name="what-are-security-alerts"></a><span data-ttu-id="c507b-109">O que são alertas de segurança?</span><span class="sxs-lookup"><span data-stu-id="c507b-109">What are security alerts?</span></span>
<span data-ttu-id="c507b-110">Central de segurança automaticamente coleta, analisa e integra dados de log de seus recursos do Azure, rede Olá e conectados soluções de parceiros, como soluções de proteção de firewall e de ponto de extremidade, ameaças reais toodetect e reduzir os falsos positivos.</span><span class="sxs-lookup"><span data-stu-id="c507b-110">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, hello network, and connected partner solutions, like firewall and endpoint protection solutions, toodetect real threats and reduce false positives.</span></span> <span data-ttu-id="c507b-111">É mostrada uma lista de alertas de segurança priorizados na Central de segurança junto com hello informações que você precisa tooquickly investigar o problema hello e recomendações sobre como tooremediate um ataque.</span><span class="sxs-lookup"><span data-stu-id="c507b-111">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem and recommendations for how tooremediate an attack.</span></span>


> [!NOTE]
> <span data-ttu-id="c507b-112">Para saber mais sobre como funciona os recursos de detecção da Central de Segurança, leia [Recursos de detecção da Central de Segurança do Azure](security-center-detection-capabilities.md).</span><span class="sxs-lookup"><span data-stu-id="c507b-112">For more information about how Security Center detection capabilities work, read [Azure Security Center Detection Capabilities](security-center-detection-capabilities.md).</span></span>
>
>

## <a name="managing-security-alerts"></a><span data-ttu-id="c507b-113">Configurando alertas de segurança</span><span class="sxs-lookup"><span data-stu-id="c507b-113">Managing security alerts</span></span>
<span data-ttu-id="c507b-114">Você pode examinar os alertas atuais examinando Olá **alertas de segurança** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="c507b-114">You can review your current alerts by looking at hello **Security alerts** tile.</span></span> <span data-ttu-id="c507b-115">Abra o Portal do Azure e siga as etapas de saudação abaixo toosee mais detalhes sobre cada alerta:</span><span class="sxs-lookup"><span data-stu-id="c507b-115">Open Azure Portal and follow hello steps below toosee more details about each alert:</span></span>

1. <span data-ttu-id="c507b-116">No painel de Central de segurança hello, você verá Olá **alertas de segurança** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="c507b-116">On hello Security Center dashboard, you will see hello **Security alerts** tile.</span></span>

    ![Bloco Alertas de segurança na Central de Segurança](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. <span data-ttu-id="c507b-118">Clique em Olá bloco tooopen Olá **alertas de segurança** folha que contém mais detalhes sobre Olá alertas conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="c507b-118">Click hello tile tooopen hello **Security alerts** blade that contains more details about hello alerts as shown below.</span></span>

   ![folha de alertas de segurança Olá na Central de segurança](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

<span data-ttu-id="c507b-120">Na parte inferior Olá esta folha são os detalhes de saudação para cada alerta.</span><span class="sxs-lookup"><span data-stu-id="c507b-120">In hello bottom part of this blade are hello details for each alert.</span></span> <span data-ttu-id="c507b-121">toosort, clique em coluna Olá que você deseja toosort por.</span><span class="sxs-lookup"><span data-stu-id="c507b-121">toosort, click hello column that you want toosort by.</span></span> <span data-ttu-id="c507b-122">definição de saudação para cada coluna é indicada abaixo:</span><span class="sxs-lookup"><span data-stu-id="c507b-122">hello definition for each column is given below:</span></span>

* <span data-ttu-id="c507b-123">**Descrição**: uma breve explicação de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="c507b-123">**Description**: A brief explanation of hello alert.</span></span>
* <span data-ttu-id="c507b-124">**Contagem**: uma lista de todos os alertas desse tipo específico que foram detectados em um dia específico.</span><span class="sxs-lookup"><span data-stu-id="c507b-124">**Count**: A list of all alerts of this specific type that were detected on a specific day.</span></span>
* <span data-ttu-id="c507b-125">**Detectado pelo**: Olá serviço que foi responsável para disparar o alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="c507b-125">**Detected by**: hello service that was responsible for triggering hello alert.</span></span>
* <span data-ttu-id="c507b-126">**Data**: Olá data que o evento Olá ocorreu.</span><span class="sxs-lookup"><span data-stu-id="c507b-126">**Date**: hello date that hello event occurred.</span></span>
* <span data-ttu-id="c507b-127">**Estado**: Olá estado atual para o alerta.</span><span class="sxs-lookup"><span data-stu-id="c507b-127">**State**: hello current state for that alert.</span></span> <span data-ttu-id="c507b-128">Há dois tipos de estado:</span><span class="sxs-lookup"><span data-stu-id="c507b-128">There are two types of states:</span></span>
  * <span data-ttu-id="c507b-129">**Active**: alerta de segurança Olá foi detectada.</span><span class="sxs-lookup"><span data-stu-id="c507b-129">**Active**: hello security alert has been detected.</span></span>
* <span data-ttu-id="c507b-130">**Severidade**: nível de severidade hello, que pode ser alta, média ou baixa.</span><span class="sxs-lookup"><span data-stu-id="c507b-130">**Severity**: hello severity level, which can be high, medium or low.</span></span>

### <a name="filtering-alerts"></a><span data-ttu-id="c507b-131">Filtragem de alertas</span><span class="sxs-lookup"><span data-stu-id="c507b-131">Filtering alerts</span></span>
<span data-ttu-id="c507b-132">Você pode filtrar com base na data, no estado e na gravidade dos alertas.</span><span class="sxs-lookup"><span data-stu-id="c507b-132">You can filter alerts based on date, state, and severity.</span></span> <span data-ttu-id="c507b-133">Filtragem de alertas pode ser útil para cenários em que você precisa que o escopo de saudação toonarrow de apresentação de alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="c507b-133">Filtering alerts can be useful for scenarios where you need toonarrow hello scope of security alerts show.</span></span> <span data-ttu-id="c507b-134">Por exemplo, você pode desejar tooaddress alertas de segurança que ocorreram em Olá últimas 24 horas, porque você está investigando uma possível falha no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="c507b-134">For example, you might you want tooaddress security alerts that occurred in hello last 24 hours because you are investigating a potential breach in hello system.</span></span>

1. <span data-ttu-id="c507b-135">Clique em **filtro** em Olá **alertas de segurança** folha.</span><span class="sxs-lookup"><span data-stu-id="c507b-135">Click **Filter** on hello **Security Alerts** blade.</span></span> <span data-ttu-id="c507b-136">Olá **filtro** folha é aberto e você selecionar valores de data, o estado e a gravidade de saudação desejar toosee.</span><span class="sxs-lookup"><span data-stu-id="c507b-136">hello **Filter** blade opens and you select hello date, state, and severity values you wish toosee.</span></span>

    ![Filtragem de alertas na Central de Segurança](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a><span data-ttu-id="c507b-138">Responder a alertas de toosecurity</span><span class="sxs-lookup"><span data-stu-id="c507b-138">Respond toosecurity alerts</span></span>
<span data-ttu-id="c507b-139">Selecione um toolearn de alerta de segurança mais sobre o evento Olá que disparou o alerta hello e, se houver, etapas que você precisam tootake tooremediate um ataque.</span><span class="sxs-lookup"><span data-stu-id="c507b-139">Select a security alert toolearn more about hello event(s) that triggered hello alert and what, if any, steps you need tootake tooremediate an attack.</span></span> <span data-ttu-id="c507b-140">Os alertas de segurança são agrupados por tipo e data.</span><span class="sxs-lookup"><span data-stu-id="c507b-140">Security alerts are grouped by type and date.</span></span> <span data-ttu-id="c507b-141">Clicando em um alerta de segurança, você abrirá uma folha que contém uma lista de alertas de saudação agrupada.</span><span class="sxs-lookup"><span data-stu-id="c507b-141">Clicking a security alert will open a blade containing a list of hello grouped alerts.</span></span>

![Responder a alertas toosecurity na Central de segurança do Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

<span data-ttu-id="c507b-143">Nesse caso, os alertas de saudação que foram acionados consulte toosuspicious atividade do protocolo de área de trabalho remota (RDP).</span><span class="sxs-lookup"><span data-stu-id="c507b-143">In this case, hello alerts that were triggered refer toosuspicious Remote Desktop Protocol (RDP) activity.</span></span> <span data-ttu-id="c507b-144">Olá primeira coluna mostra quais recursos foram atacados; Olá segundo mostra quantas vezes recurso Olá atacado; Olá terceiro mostra o tempo de saudação de ataque de saudação. Olá quarto mostra o estado de alerta de saudação; e Olá quinto mostra a gravidade de saudação do ataque de saudação.</span><span class="sxs-lookup"><span data-stu-id="c507b-144">hello first column shows which resources were attacked; hello second shows how many times hello resource was attacked; hello third shows hello time of hello attack; hello fourth shows state of hello alert; and hello fifth shows hello severity of hello attack.</span></span> <span data-ttu-id="c507b-145">Depois de revisar essas informações, clique em recursos de saudação que foi atacado e abrirá uma nova folha.</span><span class="sxs-lookup"><span data-stu-id="c507b-145">After reviewing this information, click hello resource that was attacked and a new blade will open.</span></span>

![Sugestões para quais toodo sobre a segurança de alertas na Central de segurança do Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

<span data-ttu-id="c507b-147">Em Olá **descrição** campo desta folha você encontrará mais detalhes sobre esse evento.</span><span class="sxs-lookup"><span data-stu-id="c507b-147">In hello **Description** field of this blade you will find more details about this event.</span></span> <span data-ttu-id="c507b-148">Esses detalhes adicionais oferecem informações sobre quais Olá disparada segurança alerta, Olá recurso de destino, quando aplicável Olá fonte de endereço IP e recomendações sobre como tooremediate.</span><span class="sxs-lookup"><span data-stu-id="c507b-148">These additional details offer insight into what triggered hello security alert, hello target resource, when applicable hello source IP address, and recommendations about how tooremediate.</span></span>  <span data-ttu-id="c507b-149">Em alguns casos, o endereço IP de origem Olá ser esvaziará (não disponível) porque nem todos os logs de eventos de segurança do Windows incluem o endereço IP de saudação.</span><span class="sxs-lookup"><span data-stu-id="c507b-149">In some instances, hello source IP address will be empty (not available) because not all Windows security events logs include hello IP address.</span></span>

<span data-ttu-id="c507b-150">correção Olá sugerida pela Central de segurança variam de acordo alerta de segurança toohello.</span><span class="sxs-lookup"><span data-stu-id="c507b-150">hello remediation suggested by Security Center will vary according toohello security alert.</span></span> <span data-ttu-id="c507b-151">Em alguns casos, você pode ter toouse tooimplement outros recursos do Azure Olá recomendado correção.</span><span class="sxs-lookup"><span data-stu-id="c507b-151">In some cases, you may have toouse other Azure capabilities tooimplement hello recommended remediation.</span></span> <span data-ttu-id="c507b-152">Olá, por exemplo, a correção para esse ataque é o endereço IP do tooblacklist Olá que está gerando esse ataque usando um [ACL de rede](../virtual-network/virtual-networks-acl.md) ou um [grupo de segurança de rede](../virtual-network/virtual-networks-nsg.md) regra.</span><span class="sxs-lookup"><span data-stu-id="c507b-152">For example, hello remediation for this attack is tooblacklist hello IP address that is generating this attack by using a [network ACL](../virtual-network/virtual-networks-acl.md) or a [network security group](../virtual-network/virtual-networks-nsg.md) rule.</span></span>

> [!NOTE]
> <span data-ttu-id="c507b-153">Para obter mais informações sobre tipos diferentes de saudação de alertas, leia [alertas de segurança por tipo na Central de segurança do Azure](security-center-alerts-type.md).</span><span class="sxs-lookup"><span data-stu-id="c507b-153">For more information on hello different types of alerts, read [Security Alerts by Type in Azure Security Center](security-center-alerts-type.md).</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="c507b-154">Consulte também</span><span class="sxs-lookup"><span data-stu-id="c507b-154">See also</span></span>
<span data-ttu-id="c507b-155">Neste documento, você aprendeu como tooconfigure políticas de segurança na Central de segurança.</span><span class="sxs-lookup"><span data-stu-id="c507b-155">In this document, you learned how tooconfigure security policies in Security Center.</span></span> <span data-ttu-id="c507b-156">toolearn mais sobre o Centro de segurança, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="c507b-156">toolearn more about Security Center, see hello following:</span></span>

* [<span data-ttu-id="c507b-157">Manipulação de incidente de segurança na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="c507b-157">Handling Security Incident in Azure Security Center</span></span>](security-center-incident.md)
* [<span data-ttu-id="c507b-158">Recursos de detecção da Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="c507b-158">Azure Security Center Detection Capabilities</span></span>](security-center-detection-capabilities.md)
* [<span data-ttu-id="c507b-159">Guia de planejamento e operações da Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="c507b-159">Azure Security Center Planning and Operations Guide</span></span>](security-center-planning-and-operations-guide.md)
* <span data-ttu-id="c507b-160">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="c507b-160">[Azure Security Center FAQ](security-center-faq.md) — Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="c507b-161">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) : encontre postagens no blog sobre conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="c507b-161">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Find blog posts about Azure security and compliance.</span></span>
