---
title: "Habilitar Grupos de Segurança de Rede na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento mostra como implementar a recomendação da Central de Segurança do Azure para **Habilitar Grupos de Segurança de Rede**."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f53ed853-ffaf-4530-a019-1906ba6f341b
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 1e034d59d8847f237fa0d4c772344d45cd618576
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="c6af3-103">Habilitar Grupos de Segurança de Rede na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="c6af3-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="c6af3-104">A Central de Segurança do Azure recomenda que você habilite um NSG (grupo de segurança de rede), se já não estiver habilitado.</span><span class="sxs-lookup"><span data-stu-id="c6af3-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="c6af3-105">Os NSGs contêm uma lista de regras de ACL (Lista de Controle de Acesso) que permitem ou negam o tráfego de rede para suas instâncias de VM em uma Rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="c6af3-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic to your VM instances in a Virtual Network.</span></span> <span data-ttu-id="c6af3-106">Os NSGs podem ser associados a sub-redes ou instâncias de VM individuais dentro dessa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="c6af3-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="c6af3-107">Quando um NSG é associado a uma sub-rede, as regras de ACL se aplicam a todas as instâncias de VM na sub-rede.</span><span class="sxs-lookup"><span data-stu-id="c6af3-107">When an NSG is associated with a subnet, the ACL rules apply to all the VM instances in that subnet.</span></span> <span data-ttu-id="c6af3-108">Além disso, o tráfego para uma VM individual pode ser restrito ainda mais por meio da associação de um NSG diretamente à VM.</span><span class="sxs-lookup"><span data-stu-id="c6af3-108">In addition, traffic to an individual VM can be restricted further by associating an NSG directly to that VM.</span></span> <span data-ttu-id="c6af3-109">Para saber mais, confira [O que é um NSG (Grupo de Segurança de Rede)?](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="c6af3-109">To learn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="c6af3-110">Se você não tiver NSGs habilitados, a Central de Segurança apresentará duas recomendações: Habilitar Grupos de Segurança de Rede em sub-redes e Habilitar Grupos de Segurança de Rede em máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="c6af3-110">If you do not have NSGs enabled, Security Center presents two recommendations to you: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="c6af3-111">Você escolhe a qual nível, sub-rede ou VM aplicar NSGs.</span><span class="sxs-lookup"><span data-stu-id="c6af3-111">You choose which level, subnet or VM, to apply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="c6af3-112">Este documento apresenta o serviço usando uma implantação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c6af3-112">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="c6af3-113">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="c6af3-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="c6af3-114">Implementar a recomendação</span><span class="sxs-lookup"><span data-stu-id="c6af3-114">Implement the recommendation</span></span>
1. <span data-ttu-id="c6af3-115">Na folha **Recomendações**, selecione **Habilitar Grupos de Segurança de Rede** em sub-redes ou em máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="c6af3-115">In the **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="c6af3-116">![Habilitar Grupos de segurança de rede][1]</span><span class="sxs-lookup"><span data-stu-id="c6af3-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="c6af3-117">Isso abrirá a folha **Configurar Grupos de Segurança de Rede Ausentes** para sub-redes ou para máquinas virtuais, dependendo da recomendação que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="c6af3-117">This opens the blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on the recommendation that you selected.</span></span> <span data-ttu-id="c6af3-118">Selecione uma sub-rede ou máquina virtual para configurar um NSG.</span><span class="sxs-lookup"><span data-stu-id="c6af3-118">Select a subnet or a virtual machine to configure an NSG on.</span></span>

   ![Configurar NSG para sub-rede][2]

   ![Configurar NSG para VM][3]
3. <span data-ttu-id="c6af3-121">Na folha **Escolher grupo de segurança de rede**, selecione um NSG existente ou selecione para **Criar novo** para criar um novo NSG.</span><span class="sxs-lookup"><span data-stu-id="c6af3-121">On the **Choose network security group** blade, select an existing NSG or select **Create new** to create an NSG.</span></span>

   ![Escolher grupo de segurança de rede][4]

<span data-ttu-id="c6af3-123">Se você criar um novo NSG, siga as etapas em [Como gerenciar NSGs usando o portal do Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) para criar um NSG e definir regras de segurança.</span><span class="sxs-lookup"><span data-stu-id="c6af3-123">If you create an NSG, follow the steps in [How to manage NSGs using the Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) to create an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="c6af3-124">Consulte também</span><span class="sxs-lookup"><span data-stu-id="c6af3-124">See also</span></span>
<span data-ttu-id="c6af3-125">Este artigo mostrou como implementar a recomendação da Central de Segurança "Habilitar Grupos de Segurança de Rede" para máquinas virtuais ou sub-redes.</span><span class="sxs-lookup"><span data-stu-id="c6af3-125">This article showed you how to implement the Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="c6af3-126">Para saber mais sobre como habilitar NSGs, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c6af3-126">To learn more about enabling NSGs, see the following:</span></span>

* [<span data-ttu-id="c6af3-127">O que é um NSG (grupo de segurança de rede)?</span><span class="sxs-lookup"><span data-stu-id="c6af3-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="c6af3-128">Como gerenciar NSGs usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c6af3-128">How to manage NSGs using the Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="c6af3-129">Para saber mais sobre a Central de Segurança, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c6af3-129">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="c6af3-130">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md) – saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6af3-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="c6af3-131">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6af3-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c6af3-132">[Monitoramento de integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md) : saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6af3-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="c6af3-133">[Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md) : aprenda a gerenciar e a responder a alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="c6af3-133">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="c6af3-134">[Monitoramento de soluções de parceiros com a Central de Segurança do Azure](security-center-partner-solutions.md) – saiba como monitorar o status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="c6af3-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="c6af3-135">[Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md) : encontre as perguntas frequentes sobre como usar o serviço de localização.</span><span class="sxs-lookup"><span data-stu-id="c6af3-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="c6af3-136">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) : obtenha as últimas notícias de segurança e informações do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6af3-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
