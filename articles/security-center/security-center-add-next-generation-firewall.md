---
title: "aaaAdd um firewall de geração Avançar na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendações da Central de segurança do Azure * * adicionar uma próxima geração Firewall * * e * * tráfego de rota somente por meio de NGFW * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 48b99015-4db8-4ce8-85e4-b544c0fa203e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9a80f12571ba08eadf3361728c6321388c863235
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-next-generation-firewall-in-azure-security-center"></a><span data-ttu-id="f57c1-103">Adicionar um Firewall de Última Geração na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="f57c1-103">Add a Next Generation Firewall in Azure Security Center</span></span>
<span data-ttu-id="f57c1-104">Central de segurança do Azure pode recomendar que você adicionar um firewall de geração de Avançar (NGFW) de um tooincrease de parceiro da Microsoft suas proteções de segurança.</span><span class="sxs-lookup"><span data-stu-id="f57c1-104">Azure Security Center may recommend that you add a next generation firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> <span data-ttu-id="f57c1-105">Este documento orienta você por um exemplo de como toodo isso.</span><span class="sxs-lookup"><span data-stu-id="f57c1-105">This document walks you through an example of how toodo this.</span></span>

> [!NOTE]
> <span data-ttu-id="f57c1-106">Este documento apresenta serviço hello usando um exemplo de implantação.</span><span class="sxs-lookup"><span data-stu-id="f57c1-106">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="f57c1-107">Ela não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="f57c1-107">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="f57c1-108">Implementar a recomendação de saudação</span><span class="sxs-lookup"><span data-stu-id="f57c1-108">Implement hello recommendation</span></span>
1. <span data-ttu-id="f57c1-109">Em Olá **recomendações** folha, selecione **adicionar um Firewall de geração de Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f57c1-109">In hello **Recommendations** blade, select **Add a Next Generation Firewall**.</span></span>
   <span data-ttu-id="f57c1-110">![Adicionar um Firewall de Última Geração][1]</span><span class="sxs-lookup"><span data-stu-id="f57c1-110">![Add a Next Generation Firewall][1]</span></span>
2. <span data-ttu-id="f57c1-111">Em Olá **adicionar um Firewall de geração de Avançar** folha, selecione um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="f57c1-111">In hello **Add a Next Generation Firewall** blade, select an endpoint.</span></span>
   <span data-ttu-id="f57c1-112">![Selecionar um ponto de extremidade][2]</span><span class="sxs-lookup"><span data-stu-id="f57c1-112">![Select an endpoint][2]</span></span>
3. <span data-ttu-id="f57c1-113">Uma segunda folha **Adicionar um Firewall de Última Geração** será aberta.</span><span class="sxs-lookup"><span data-stu-id="f57c1-113">A second **Add a Next Generation Firewall** blade opens.</span></span> <span data-ttu-id="f57c1-114">Você pode escolher toouse uma solução existente se estiver disponível ou você pode criar um novo.</span><span class="sxs-lookup"><span data-stu-id="f57c1-114">You can choose toouse an existing solution if available or you can create a new one.</span></span> <span data-ttu-id="f57c1-115">Neste exemplo não existem soluções disponíveis, por isso, criaremos um novo NGFW.</span><span class="sxs-lookup"><span data-stu-id="f57c1-115">In this example, there are no existing solutions available so we create an NGFW.</span></span>
   <span data-ttu-id="f57c1-116">![Criar um novo Firewall de Última Geração][3]</span><span class="sxs-lookup"><span data-stu-id="f57c1-116">![Create Next Generation Firewall][3]</span></span>
4. <span data-ttu-id="f57c1-117">toocreate um NGFW, selecione uma solução de lista de saudação de parceiros integrados.</span><span class="sxs-lookup"><span data-stu-id="f57c1-117">toocreate an NGFW, select a solution from hello list of integrated partners.</span></span> <span data-ttu-id="f57c1-118">Neste exemplo, selecionamos **Check Point**.</span><span class="sxs-lookup"><span data-stu-id="f57c1-118">In this example, we select **Check Point**.</span></span>
   <span data-ttu-id="f57c1-119">![Selecionar uma solução de Firewall de Última Geração][4]</span><span class="sxs-lookup"><span data-stu-id="f57c1-119">![Select Next Generation Firewall solution][4]</span></span>
5. <span data-ttu-id="f57c1-120">Olá **ponto de verificação** folha é aberto, fornecendo informações sobre solução de parceiro hello.</span><span class="sxs-lookup"><span data-stu-id="f57c1-120">hello **Check Point** blade opens providing you information about hello partner solution.</span></span> <span data-ttu-id="f57c1-121">Selecione **criar** na folha de informações de saudação.</span><span class="sxs-lookup"><span data-stu-id="f57c1-121">Select **Create** in hello information blade.</span></span>
   <span data-ttu-id="f57c1-122">![Folha Informações do firewall][5]</span><span class="sxs-lookup"><span data-stu-id="f57c1-122">![Firewall information blade][5]</span></span>
6. <span data-ttu-id="f57c1-123">Olá **criar a máquina virtual** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="f57c1-123">hello **Create virtual machine** blade opens.</span></span> <span data-ttu-id="f57c1-124">Aqui você pode inserir informações necessária toospin uma máquina virtual (VM) que executa Olá NGFW.</span><span class="sxs-lookup"><span data-stu-id="f57c1-124">Here you can enter information required toospin up a virtual machine (VM) that runs hello NGFW.</span></span> <span data-ttu-id="f57c1-125">Siga as etapas de saudação e fornecer Olá NGFW informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="f57c1-125">Follow hello steps and provide hello NGFW information required.</span></span> <span data-ttu-id="f57c1-126">Selecione tooapply Okey.</span><span class="sxs-lookup"><span data-stu-id="f57c1-126">Select OK tooapply.</span></span>
   <span data-ttu-id="f57c1-127">![Criar a máquina virtual toorun NGFW][6]</span><span class="sxs-lookup"><span data-stu-id="f57c1-127">![Create virtual machine toorun NGFW][6]</span></span>

## <a name="route-traffic-through-ngfw-only"></a><span data-ttu-id="f57c1-128">Rotear o tráfego apenas através do NGFW</span><span class="sxs-lookup"><span data-stu-id="f57c1-128">Route traffic through NGFW only</span></span>
<span data-ttu-id="f57c1-129">Retornar toohello **recomendações** folha.</span><span class="sxs-lookup"><span data-stu-id="f57c1-129">Return toohello **Recommendations** blade.</span></span> <span data-ttu-id="f57c1-130">Uma nova entrada foi gerada após a adição de um NGFW por meio da Central de Segurança, chamada **Rotear o tráfego somente por meio do NGFW**.</span><span class="sxs-lookup"><span data-stu-id="f57c1-130">A new entry was generated after you added an NGFW via Security Center, called **Route traffic through NGFW only**.</span></span> <span data-ttu-id="f57c1-131">Essa recomendação será criada somente se você tiver instalado o NGFW por meio da Central de Segurança.</span><span class="sxs-lookup"><span data-stu-id="f57c1-131">This recommendation is created only if you installed your NGFW through Security Center.</span></span> <span data-ttu-id="f57c1-132">Se você tiver pontos de extremidade para a Internet, a Central de segurança recomenda que você configure regras de grupo de segurança de rede que forçar o tráfego de entrada tooyour VM por meio de seu NGFW.</span><span class="sxs-lookup"><span data-stu-id="f57c1-132">If you have Internet-facing endpoints, Security Center recommends that you configure Network Security Group rules that force inbound traffic tooyour VM through your NGFW.</span></span>

1. <span data-ttu-id="f57c1-133">Em Olá **folha recomendações**, selecione **rotear o tráfego por meio de NGFW**.</span><span class="sxs-lookup"><span data-stu-id="f57c1-133">In hello **Recommendations blade**, select **Route traffic through NGFW only**.</span></span>
   <span data-ttu-id="f57c1-134">![Rotear o tráfego apenas através do NGFW][7]</span><span class="sxs-lookup"><span data-stu-id="f57c1-134">![Route traffic through NGFW only][7]</span></span>
2. <span data-ttu-id="f57c1-135">Isso abre a folha de saudação **rotear o tráfego por meio de NGFW**, que lista as VMs que você pode rotear o tráfego.</span><span class="sxs-lookup"><span data-stu-id="f57c1-135">This opens hello blade **Route traffic through NGFW only**, which lists VMs that you can route traffic to.</span></span> <span data-ttu-id="f57c1-136">Selecione uma VM na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="f57c1-136">Select a VM from hello list.</span></span>
   <span data-ttu-id="f57c1-137">![Selecionar uma máquina virtual][8]</span><span class="sxs-lookup"><span data-stu-id="f57c1-137">![Select a VM][8]</span></span>
3. <span data-ttu-id="f57c1-138">Uma folha de saudação selecionado VM é aberta, exibindo as regras de entrada relacionadas.</span><span class="sxs-lookup"><span data-stu-id="f57c1-138">A blade for hello selected VM opens, displaying related inbound rules.</span></span> <span data-ttu-id="f57c1-139">Uma descrição fornece a você mais informações sobre as próximas etapas possíveis.</span><span class="sxs-lookup"><span data-stu-id="f57c1-139">A description provides you with more information on possible next steps.</span></span> <span data-ttu-id="f57c1-140">Selecione **editar regras de entrada** tooproceed com a edição de uma regra de entrada.</span><span class="sxs-lookup"><span data-stu-id="f57c1-140">Select **Edit inbound rules** tooproceed with editing an inbound rule.</span></span> <span data-ttu-id="f57c1-141">Olá expectativa é que **fonte** não está definido muito**qualquer** para pontos de extremidade do hello voltados para Internet vinculado com hello NGFW.</span><span class="sxs-lookup"><span data-stu-id="f57c1-141">hello expectation is that **Source** is not set too**Any** for hello Internet-facing endpoints linked with hello NGFW.</span></span> <span data-ttu-id="f57c1-142">toolearn mais informações sobre propriedades de saudação de regra de entrada hello, consulte [regras NSG](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span><span class="sxs-lookup"><span data-stu-id="f57c1-142">toolearn more about hello properties of hello inbound rule, see [NSG rules](../virtual-network/virtual-networks-nsg.md#nsg-rules).</span></span>
   <span data-ttu-id="f57c1-143">![Configurar o acesso de toolimit regras][9]
   ![Editar regra de entrada][10]</span><span class="sxs-lookup"><span data-stu-id="f57c1-143">![Configure rules toolimit access][9]
![Edit inbound rule][10]</span></span>

## <a name="see-also"></a><span data-ttu-id="f57c1-144">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f57c1-144">See also</span></span>
<span data-ttu-id="f57c1-145">Este documento lhe mostrou como tooimplement Olá recomendação da Central de segurança "Adicionar um Firewall de geração Avançar".</span><span class="sxs-lookup"><span data-stu-id="f57c1-145">This document showed you how tooimplement hello Security Center recommendation "Add a Next Generation Firewall."</span></span> <span data-ttu-id="f57c1-146">toolearn mais sobre NGFWs e hello solução de parceiro do ponto de verificação, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="f57c1-146">toolearn more about NGFWs and hello Check Point partner solution, see hello following:</span></span>

* [<span data-ttu-id="f57c1-147">Firewall de Última Geração</span><span class="sxs-lookup"><span data-stu-id="f57c1-147">Next-Generation Firewall</span></span>](https://en.wikipedia.org/wiki/Next-Generation_Firewall)
* [<span data-ttu-id="f57c1-148">Check Point vSEC</span><span class="sxs-lookup"><span data-stu-id="f57c1-148">Check Point vSEC</span></span>](https://azure.microsoft.com/marketplace/partners/checkpoint/check-point-r77-10/)

<span data-ttu-id="f57c1-149">toolearn mais sobre o Centro de segurança, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="f57c1-149">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="f57c1-150">[Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança.</span><span class="sxs-lookup"><span data-stu-id="f57c1-150">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="f57c1-151">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f57c1-151">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="f57c1-152">[Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f57c1-152">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="f57c1-153">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="f57c1-153">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="f57c1-154">[Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="f57c1-154">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="f57c1-155">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="f57c1-155">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="f57c1-156">[Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – encontre postagens no blog sobre conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="f57c1-156">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-add-next-gen-firewall/add-next-gen-firewall.png
[2]: ./media/security-center-add-next-gen-firewall/select-an-endpoint.png
[3]: ./media/security-center-add-next-gen-firewall/create-new-next-gen-firewall.png
[4]: ./media/security-center-add-next-gen-firewall/select-next-gen-firewall.png
[5]: ./media/security-center-add-next-gen-firewall/firewall-solution-info-blade.png
[6]: ./media/security-center-add-next-gen-firewall/create-virtual-machine.png
[7]: ./media/security-center-add-next-gen-firewall/route-traffic-through-ngfw.png
[8]: ./media/security-center-add-next-gen-firewall/select-vm.png
[9]: ./media/security-center-add-next-gen-firewall/configure-rules-to-limit-access.png
[10]: ./media/security-center-add-next-gen-firewall/edit-inbound-rule.png
