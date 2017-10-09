---
title: "aaaRestrict acesso por meio de pontos de extremidade da Internet na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * restringir o acesso por meio da Internet voltada para o ponto de extremidade * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 727d88c9-163b-4ea0-a4ce-3be43686599f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: ee72497088618d4db29b5ae4183f4fe77b498423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="7bbc3-103">Restringir o acesso por meio de pontos de extremidade para a Internet na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="7bbc3-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="7bbc3-104">A Central de Segurança do Azure recomendará que você restrinja o acesso por meio de pontos de extremidade para a Internet se qualquer um dos seus grupos de segurança de rede (NSGs) tiver uma ou mais regras de entrada que permitam acesso de "qualquer" endereço IP de origem.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="7bbc3-105">Abertura de acesso muito "qualquer" pode permitir que os invasores tooaccess seus recursos.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-105">Opening access too“any” may enable attackers tooaccess your resources.</span></span> <span data-ttu-id="7bbc3-106">Central de segurança recomende que você editar endereços IP essas regras de entrada toorestrict acesso toosource que realmente precisam de acesso.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-106">Security Center will recommend that you edit these inbound rules toorestrict access toosource IP addresses that actually need access.</span></span>

<span data-ttu-id="7bbc3-107">Essa recomendação é gerada para qualquer porta que não seja da Web que tenha "qualquer" como fonte.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="7bbc3-108">Este documento apresenta serviço hello usando um exemplo de implantação.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="7bbc3-109">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="7bbc3-110">Implementar a recomendação de saudação</span><span class="sxs-lookup"><span data-stu-id="7bbc3-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="7bbc3-111">Em Olá **folha recomendações**, selecione **restringir o acesso por meio do ponto de extremidade da Internet**.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-111">In hello **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![Restringir o acesso por meio de ponto de extremidade para a Internet][1]
2. <span data-ttu-id="7bbc3-113">Isso abre a folha de saudação **restringir o acesso por meio do ponto de extremidade da Internet**.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-113">This opens hello blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="7bbc3-114">Esta folha lista Olá as máquinas virtuais (VMs) com as regras de entrada que cria um problema de segurança potencial.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-114">This blade lists hello virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="7bbc3-115">Selecionar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-115">Select a VM.</span></span>

   ![Selecionar uma máquina virtual][2]
3. <span data-ttu-id="7bbc3-117">Olá **NSG** folha exibe informações de grupo de segurança de rede, as regras de entrada relacionadas, e Olá associados a VM.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-117">hello **NSG** blade displays Network Security Group information, related inbound rules, and hello associated VM.</span></span> <span data-ttu-id="7bbc3-118">Selecione **editar regras de entrada** tooproceed com a edição de uma regra de entrada.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-118">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span>

   ![Folha Grupo de Segurança de Rede][3]
4. <span data-ttu-id="7bbc3-120">Em Olá **regras de segurança de entrada** selecione folha Olá tooedit de regra de entrada.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-120">On hello **Inbound security rules** blade select hello inbound rule tooedit.</span></span> <span data-ttu-id="7bbc3-121">Neste exemplo, vamos selecionar **AllowWeb**.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-121">In this example, let’s select **AllowWeb**.</span></span>

   ![Regras de segurança de entrada][4]

   <span data-ttu-id="7bbc3-123">Observe que você também pode selecionar **padrão regras** toosee conjunto de saudação de regras padrão por todos os NSGs.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-123">Note, you can also select **Default rules** toosee hello set of default rules contained by all NSGs.</span></span> <span data-ttu-id="7bbc3-124">as regras de saudação padrão não podem ser excluídas, mas, porque eles recebem uma prioridade mais baixa, elas podem ser substituídas pelas regras de saudação que você criar.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-124">hello default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by hello rules that you create.</span></span> <span data-ttu-id="7bbc3-125">Saiba mais sobre [regras padrão](../virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="7bbc3-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![Regras padrão][5]
5. <span data-ttu-id="7bbc3-127">Em Olá **AllowWeb** folha, editar propriedades de saudação da regra de entrada hello para que Olá **origem** é um endereço IP ou o bloco de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-127">On hello **AllowWeb** blade, edit hello properties of hello inbound rule so that hello **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="7bbc3-128">toolearn mais informações sobre propriedades de saudação de regra de entrada hello, consulte [regras NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="7bbc3-128">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![Editar regra de entrada][6]

## <a name="see-also"></a><span data-ttu-id="7bbc3-130">Consulte também</span><span class="sxs-lookup"><span data-stu-id="7bbc3-130">See also</span></span>
<span data-ttu-id="7bbc3-131">Este artigo lhe mostrou como tooimplement Olá Central de segurança recomendação "restringir o acesso por meio do ponto de extremidade da Internet."</span><span class="sxs-lookup"><span data-stu-id="7bbc3-131">This article showed you how tooimplement hello Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="7bbc3-132">toolearn mais sobre como habilitar os NSGs e regras, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="7bbc3-132">toolearn more about enabling NSGs and rules, see hello following:</span></span>

* [<span data-ttu-id="7bbc3-133">O que é um NSG (grupo de segurança de rede)?</span><span class="sxs-lookup"><span data-stu-id="7bbc3-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="7bbc3-134">Como toomanage NSGs usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7bbc3-134">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="7bbc3-135">toolearn mais sobre o Centro de segurança, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="7bbc3-135">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="7bbc3-136">[Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md)– Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="7bbc3-137">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="7bbc3-138">[Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md)– Saiba como toomonitor Olá a integridade de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="7bbc3-139">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md)– Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-139">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="7bbc3-140">[Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="7bbc3-141">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md)– localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="7bbc3-142">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/)– obter notícias mais recentes de segurança do Azure hello e informações.</span><span class="sxs-lookup"><span data-stu-id="7bbc3-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
