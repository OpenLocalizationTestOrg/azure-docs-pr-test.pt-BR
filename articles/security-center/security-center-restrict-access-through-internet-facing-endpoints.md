---
title: "Restringir o acesso por meio de pontos de extremidade para a Internet na Central de Segurança do Azure | Microsoft Docs"
description: "Este artigo mostrou como implementar a recomendação da Central de Segurança do Azure **Restringir o acesso por meio de ponto de extremidade para a Internet**."
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
ms.openlocfilehash: f7309c617f1705205e2c9f1b1b48d141391d45da
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="restrict-access-through-internet-facing-endpoints-in-azure-security-center"></a><span data-ttu-id="e5d80-103">Restringir o acesso por meio de pontos de extremidade para a Internet na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="e5d80-103">Restrict access through Internet-facing endpoints in Azure Security Center</span></span>
<span data-ttu-id="e5d80-104">A Central de Segurança do Azure recomendará que você restrinja o acesso por meio de pontos de extremidade para a Internet se qualquer um dos seus grupos de segurança de rede (NSGs) tiver uma ou mais regras de entrada que permitam acesso de "qualquer" endereço IP de origem.</span><span class="sxs-lookup"><span data-stu-id="e5d80-104">Azure Security Center will recommend that you restrict access through Internet-facing endpoints if any of your Network Security Groups (NSGs) has one or more inbound rules that allow access from “any” source IP address.</span></span> <span data-ttu-id="e5d80-105">Abrir o acesso a "qualquer" um pode permitir que os invasores acessem seus recursos.</span><span class="sxs-lookup"><span data-stu-id="e5d80-105">Opening access to “any” may enable attackers to access your resources.</span></span> <span data-ttu-id="e5d80-106">A Central de Segurança recomendará que você edite essas regras de entrada para restringir o acesso a endereços IP de origem que realmente precisem de acesso.</span><span class="sxs-lookup"><span data-stu-id="e5d80-106">Security Center will recommend that you edit these inbound rules to restrict access to source IP addresses that actually need access.</span></span>

<span data-ttu-id="e5d80-107">Essa recomendação é gerada para qualquer porta que não seja da Web que tenha "qualquer" como fonte.</span><span class="sxs-lookup"><span data-stu-id="e5d80-107">This recommendation is generated for any non-web port that has "any" as source.</span></span>

> [!NOTE]
> <span data-ttu-id="e5d80-108">Este documento apresenta o serviço usando uma implantação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="e5d80-108">This document introduces the service by using an example deployment.</span></span> <span data-ttu-id="e5d80-109">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="e5d80-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="e5d80-110">Implementar a recomendação</span><span class="sxs-lookup"><span data-stu-id="e5d80-110">Implement the recommendation</span></span>
1. <span data-ttu-id="e5d80-111">Na folha **Recomendações**, selecione **Restringir o acesso por meio de ponto de extremidade para a Internet**.</span><span class="sxs-lookup"><span data-stu-id="e5d80-111">In the **Recommendations blade**, select **Restrict access through Internet facing endpoint**.</span></span>

   ![Restringir o acesso por meio de ponto de extremidade para a Internet][1]
2. <span data-ttu-id="e5d80-113">Isso abre a folha **Restringir o acesso por meio de ponto de extremidade para a Internet**.</span><span class="sxs-lookup"><span data-stu-id="e5d80-113">This opens the blade **Restrict access through Internet facing endpoint**.</span></span> <span data-ttu-id="e5d80-114">Essa folha lista as VMs (máquinas virtuais) com as regras de entrada que criam um problema potencial de segurança.</span><span class="sxs-lookup"><span data-stu-id="e5d80-114">This blade lists the virtual machines (VMs) with inbound rules that create a potential security issue.</span></span> <span data-ttu-id="e5d80-115">Selecione uma VM.</span><span class="sxs-lookup"><span data-stu-id="e5d80-115">Select a VM.</span></span>

   ![Selecionar uma máquina virtual][2]
3. <span data-ttu-id="e5d80-117">A folha **NSG** exibe informações de Grupo de Segurança de Rede, as regras de entrada relacionadas e a VM associada.</span><span class="sxs-lookup"><span data-stu-id="e5d80-117">The **NSG** blade displays Network Security Group information, related inbound rules, and the associated VM.</span></span> <span data-ttu-id="e5d80-118">Selecione **Editar regras de entrada** para prosseguir com a edição de uma regra de entrada.</span><span class="sxs-lookup"><span data-stu-id="e5d80-118">Select **Edit inbound rules** to proceed with editing an inbound rule.</span></span>

   ![Folha Grupo de Segurança de Rede][3]
4. <span data-ttu-id="e5d80-120">Na folha **Regras de segurança de entrada** , selecione a regra de entrada a editar.</span><span class="sxs-lookup"><span data-stu-id="e5d80-120">On the **Inbound security rules** blade select the inbound rule to edit.</span></span> <span data-ttu-id="e5d80-121">Neste exemplo, vamos selecionar **AllowWeb**.</span><span class="sxs-lookup"><span data-stu-id="e5d80-121">In this example, let’s select **AllowWeb**.</span></span>

   ![Regras de segurança de entrada][4]

   <span data-ttu-id="e5d80-123">Observe que você também pode selecionar **Regras padrão** para ver o conjunto de regras padrão contidas em todos os NSGs.</span><span class="sxs-lookup"><span data-stu-id="e5d80-123">Note, you can also select **Default rules** to see the set of default rules contained by all NSGs.</span></span> <span data-ttu-id="e5d80-124">As regras padrão não podem ser excluídas, mas como recebem uma prioridade mais baixa, elas podem ser substituídas pelas regras que você criar.</span><span class="sxs-lookup"><span data-stu-id="e5d80-124">The default rules cannot be deleted but, because they are assigned a lower priority, they can be overridden by the rules that you create.</span></span> <span data-ttu-id="e5d80-125">Saiba mais sobre [regras padrão](../virtual-network/virtual-networks-nsg.md#default-rules).</span><span class="sxs-lookup"><span data-stu-id="e5d80-125">Learn more about [default rules](../virtual-network/virtual-networks-nsg.md#default-rules).</span></span>

   ![Regras padrão][5]
5. <span data-ttu-id="e5d80-127">Na folha **AllowWeb**, edite as propriedades da regra de entrada para que a **Origem** seja um endereço IP ou bloco de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="e5d80-127">On the **AllowWeb** blade, edit the properties of the inbound rule so that the **Source** is an IP address or block of IP addresses.</span></span> <span data-ttu-id="e5d80-128">Para saber mais sobre as propriedades da regra de entrada, consulte [Regras de NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="e5d80-128">To learn more about the properties of the inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>

   ![Editar regra de entrada][6]

## <a name="see-also"></a><span data-ttu-id="e5d80-130">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e5d80-130">See also</span></span>
<span data-ttu-id="e5d80-131">Este artigo mostrou como implementar a recomendação da Central de Segurança "Restringir o acesso por meio de ponto de extremidade para a Internet".</span><span class="sxs-lookup"><span data-stu-id="e5d80-131">This article showed you how to implement the Security Center recommendation "Restrict access through Internet facing endpoint.”</span></span> <span data-ttu-id="e5d80-132">Para saber mais sobre como habilitar NSGs e regras, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e5d80-132">To learn more about enabling NSGs and rules, see the following:</span></span>

* [<span data-ttu-id="e5d80-133">O que é um NSG (grupo de segurança de rede)?</span><span class="sxs-lookup"><span data-stu-id="e5d80-133">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="e5d80-134">Como gerenciar NSGs usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e5d80-134">How to manage NSGs using the Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="e5d80-135">Para saber mais sobre a Central de Segurança, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e5d80-135">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="e5d80-136">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md): saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5d80-136">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="e5d80-137">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5d80-137">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="e5d80-138">[Monitoramento de integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md): saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5d80-138">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="e5d80-139">[Gerenciar e responder aos alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md): aprenda a gerenciar e responder aos alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="e5d80-139">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="e5d80-140">[Monitorar as soluções de parceiros com a Central de Segurança do Azure](security-center-partner-solutions.md) : saiba como monitorar o status de integridade de suas soluções de parceiros.</span><span class="sxs-lookup"><span data-stu-id="e5d80-140">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="e5d80-141">[Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md): encontre perguntas frequentes sobre como usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="e5d80-141">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="e5d80-142">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/): obtenha as últimas notícias de segurança e informações do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5d80-142">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/restrict-access-thru-internet-facing-endpoint.png
[2]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/select-a-vm.png
[3]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/network-security-group-blade.png
[4]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/inbound-security-rules.png
[5]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/default-rules.png
[6]: ./media/security-center-restrict-access-thru-internet-facing-endpoint/edit-inbound-rule.png
