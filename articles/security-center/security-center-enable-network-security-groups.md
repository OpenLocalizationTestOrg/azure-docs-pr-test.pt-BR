---
title: "aaaEnable grupos de segurança de rede na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * habilitar rede segurança grupos * *."
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
ms.openlocfilehash: 2f70fe432aa452f833a5c322d13102ebbd6dbb69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-network-security-groups-in-azure-security-center"></a><span data-ttu-id="f9c2c-103">Habilitar Grupos de Segurança de Rede na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="f9c2c-103">Enable Network Security Groups in Azure Security Center</span></span>
<span data-ttu-id="f9c2c-104">A Central de Segurança do Azure recomenda que você habilite um NSG (grupo de segurança de rede), se já não estiver habilitado.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-104">Azure Security Center recommends that you enable a network security group (NSG) if one is not already enabled.</span></span> <span data-ttu-id="f9c2c-105">Os NSGs contém uma lista de regras de lista de controle de acesso (ACL) que permitem ou negam o tráfego de rede tooyour instâncias VM em uma rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-105">NSGs contain a list of Access Control List (ACL) rules that allow or deny network traffic tooyour VM instances in a Virtual Network.</span></span> <span data-ttu-id="f9c2c-106">Os NSGs podem ser associados a sub-redes ou instâncias de VM individuais dentro dessa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-106">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="f9c2c-107">Quando um NSG está associado uma sub-rede, regras de ACL de saudação se aplicam a instâncias de VM Olá tooall nessa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-107">When an NSG is associated with a subnet, hello ACL rules apply tooall hello VM instances in that subnet.</span></span> <span data-ttu-id="f9c2c-108">Além disso, o tráfego tooan VM individual pode ser restrito adicional associando um NSG toothat VM diretamente.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-108">In addition, traffic tooan individual VM can be restricted further by associating an NSG directly toothat VM.</span></span> <span data-ttu-id="f9c2c-109">toolearn mais ver [o que é um grupo de segurança de rede (NSG)?](../virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="f9c2c-109">toolearn more see [What is a Network Security Group (NSG)?](../virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="f9c2c-110">Se você não tiver os NSGs habilitados, a Central de segurança apresenta dois tooyou de recomendações: habilitar os grupos de segurança de rede em sub-redes e habilitar os grupos de segurança de rede em máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-110">If you do not have NSGs enabled, Security Center presents two recommendations tooyou: Enable Network Security Groups on subnets and Enable Network Security Groups on virtual machines.</span></span> <span data-ttu-id="f9c2c-111">Você escolhe qual nível, a sub-rede ou a VM, tooapply NSGs.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-111">You choose which level, subnet or VM, tooapply NSGs.</span></span>

> [!NOTE]
> <span data-ttu-id="f9c2c-112">Este documento apresenta serviço hello usando um exemplo de implantação.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-112">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="f9c2c-113">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-113">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="f9c2c-114">Implementar a recomendação de saudação</span><span class="sxs-lookup"><span data-stu-id="f9c2c-114">Implement hello recommendation</span></span>
1. <span data-ttu-id="f9c2c-115">Em Olá **recomendações** folha, selecione **habilitar grupos de segurança de rede** em sub-redes ou em máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-115">In hello **Recommendations** blade, select **Enable Network Security Groups** on subnets or on virtual machines.</span></span>
   <span data-ttu-id="f9c2c-116">![Habilitar Grupos de segurança de rede][1]</span><span class="sxs-lookup"><span data-stu-id="f9c2c-116">![Enable Network Security Groups][1]</span></span>
2. <span data-ttu-id="f9c2c-117">Isso abre a folha de saudação **configurar grupos de segurança de rede ausente** para sub-redes ou para máquinas virtuais, dependendo de recomendação de saudação que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-117">This opens hello blade **Configure Missing Network Security Groups** for subnets or for virtual machines, depending on hello recommendation that you selected.</span></span> <span data-ttu-id="f9c2c-118">Selecione uma sub-rede ou uma máquina virtual de tooconfigure um NSG.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-118">Select a subnet or a virtual machine tooconfigure an NSG on.</span></span>

   ![Configurar NSG para sub-rede][2]

   ![Configurar NSG para VM][3]
3. <span data-ttu-id="f9c2c-121">Em Olá **o grupo de segurança de rede escolha** folha, selecione um NSG existente ou selecione **criar novo** toocreate um NSG.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-121">On hello **Choose network security group** blade, select an existing NSG or select **Create new** toocreate an NSG.</span></span>

   ![Escolher grupo de segurança de rede][4]

<span data-ttu-id="f9c2c-123">Se você criar um NSG, siga as etapas de saudação em [como toomanage NSGs usando Olá portal do Azure](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate um NSG e defina as regras de segurança.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-123">If you create an NSG, follow hello steps in [How toomanage NSGs using hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md) toocreate an NSG and set security rules.</span></span>

## <a name="see-also"></a><span data-ttu-id="f9c2c-124">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f9c2c-124">See also</span></span>
<span data-ttu-id="f9c2c-125">Este artigo mostrou como tooimplement Olá Central de segurança recomendação "habilitar grupos de segurança rede" em sub-redes ou máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-125">This article showed you how tooimplement hello Security Center recommendation "Enable Network Security Groups" for subnets or virtual machines.</span></span> <span data-ttu-id="f9c2c-126">toolearn mais sobre como habilitar os NSGs, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="f9c2c-126">toolearn more about enabling NSGs, see hello following:</span></span>

* [<span data-ttu-id="f9c2c-127">O que é um NSG (grupo de segurança de rede)?</span><span class="sxs-lookup"><span data-stu-id="f9c2c-127">What is a Network Security Group (NSG)?</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="f9c2c-128">Como toomanage NSGs usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f9c2c-128">How toomanage NSGs using hello Azure portal</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)

<span data-ttu-id="f9c2c-129">toolearn mais sobre o Centro de segurança, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="f9c2c-129">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="f9c2c-130">[Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="f9c2c-131">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="f9c2c-132">[Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="f9c2c-133">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="f9c2c-134">[Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="f9c2c-135">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="f9c2c-136">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – obter notícias mais recentes de segurança do Azure hello e informações.</span><span class="sxs-lookup"><span data-stu-id="f9c2c-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-nsg/enable-nsg.png
[2]:./media/security-center-enable-nsg/configure-nsg-for-subnet.png
[3]: ./media/security-center-enable-nsg/configure-nsg-for-vm.png
[4]: ./media/security-center-enable-nsg/choose-nsg.png
