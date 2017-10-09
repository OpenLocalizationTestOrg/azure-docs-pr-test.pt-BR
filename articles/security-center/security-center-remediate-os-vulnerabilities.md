---
title: "vulnerabilidades aaaRemediate SO na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * OS corrigir vulnerabilidades * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="12493-103">Corrigir as vulnerabilidades do sistema operacional na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="12493-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="12493-104">Central de segurança do Azure diariamente analisa o sistema de operacional de máquina virtual (VM) (SO) para as configurações que podem fazer Olá VM alterações de configuração de tooattack e recomenda mais vulnerável tooaddress essas vulnerabilidades.</span><span class="sxs-lookup"><span data-stu-id="12493-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make hello VM more vulnerable tooattack and recommends configuration changes tooaddress these vulnerabilities.</span></span> <span data-ttu-id="12493-105">Central de segurança recomenda que você resolver vulnerabilidades quando configuração do sistema operacional da VM não corresponde a saudação recomendada regras de configuração.</span><span class="sxs-lookup"><span data-stu-id="12493-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match hello recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="12493-106">Para obter mais informações sobre configurações específicas de saudação que estão sendo monitorados, consulte Olá [lista de regras de configuração recomendada](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="12493-106">For more information on hello specific configurations being monitored, see hello [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="12493-107">Implementar a recomendação de saudação</span><span class="sxs-lookup"><span data-stu-id="12493-107">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="12493-108">Este documento apresenta serviço hello usando um exemplo de implantação.</span><span class="sxs-lookup"><span data-stu-id="12493-108">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="12493-109">Este documento não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="12493-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="12493-110">Em Olá **recomendações** folha, selecione **vulnerabilidades do sistema operacional corrigir**.</span><span class="sxs-lookup"><span data-stu-id="12493-110">In hello **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="12493-111">![Corrigir as vulnerabilidades do sistema operacional][1]</span><span class="sxs-lookup"><span data-stu-id="12493-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="12493-112">Olá **vulnerabilidades do sistema operacional corrigir** folha é aberta e lista suas VMs com configurações de sistema operacional que não correspondem a saudação recomendada regras de configuração.</span><span class="sxs-lookup"><span data-stu-id="12493-112">hello **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match hello recommended configuration rules.</span></span>  <span data-ttu-id="12493-113">Para cada VM, folha Olá identifica:</span><span class="sxs-lookup"><span data-stu-id="12493-113">For each VM, hello blade identifies:</span></span>

   * <span data-ttu-id="12493-114">**REGRAS de falha** -Olá número de regras que Olá a configuração do sistema operacional da VM com falha.</span><span class="sxs-lookup"><span data-stu-id="12493-114">**FAILED RULES** -- hello number of rules that hello VM's OS configuration failed.</span></span>
   * <span data-ttu-id="12493-115">**HORA da última verificação** - date de hello e o tempo que a Central de segurança verificado pela última vez configuração do sistema operacional da VM hello.</span><span class="sxs-lookup"><span data-stu-id="12493-115">**LAST SCAN TIME** -- hello date and time that Security Center last scanned hello VM’s OS configuration.</span></span>
   * <span data-ttu-id="12493-116">**ESTADO** -Olá o estado atual da vulnerabilidade hello:</span><span class="sxs-lookup"><span data-stu-id="12493-116">**STATE** -- hello current state of hello vulnerability:</span></span>

     * <span data-ttu-id="12493-117">Abrir: vulnerabilidade Olá não tratada ainda</span><span class="sxs-lookup"><span data-stu-id="12493-117">Open: hello vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="12493-118">Em andamento: Vulnerabilidade hello está sendo aplicada no momento, nenhuma ação é necessária por você</span><span class="sxs-lookup"><span data-stu-id="12493-118">In Progress: hello vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="12493-119">Resolvido: vulnerabilidade Olá já foi abordada (quando Olá problema terá sido resolvido, entrada hello está esmaecida)</span><span class="sxs-lookup"><span data-stu-id="12493-119">Resolved: hello vulnerability was already addressed (when hello issue has been resolved, hello entry is grayed out)</span></span>
   * <span data-ttu-id="12493-120">**SEVERIDADE** – todas as vulnerabilidades são definidas tooa severidade baixa, indicando uma vulnerabilidade deve ser resolvida, mas não exigem atenção imediata.</span><span class="sxs-lookup"><span data-stu-id="12493-120">**SEVERITY** -- All vulnerabilities are set tooa severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="12493-121">Selecionar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="12493-121">Select a VM.</span></span> <span data-ttu-id="12493-122">Uma folha para que o VM abre e exibe as regras de saudação que falharam.</span><span class="sxs-lookup"><span data-stu-id="12493-122">A blade for that VM opens and displays hello rules that have failed.</span></span>
   <span data-ttu-id="12493-123">![Regras de configuração que falharam][2]</span><span class="sxs-lookup"><span data-stu-id="12493-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="12493-124">Selecione uma regra.</span><span class="sxs-lookup"><span data-stu-id="12493-124">Select a rule.</span></span> <span data-ttu-id="12493-125">Neste exemplo, você pode selecionar **A senha deve atender a requisitos de complexidade**.</span><span class="sxs-lookup"><span data-stu-id="12493-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="12493-126">Uma folha abre descrevendo impacto de regra e Olá Olá falhado.</span><span class="sxs-lookup"><span data-stu-id="12493-126">A blade opens describing hello failed rule and hello impact.</span></span> <span data-ttu-id="12493-127">Examine os detalhes de saudação e considere como são aplicadas as configurações do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="12493-127">Review hello details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="12493-128">![Descrição para a regra com falha Olá][3]</span><span class="sxs-lookup"><span data-stu-id="12493-128">![Description for hello failed rule][3]</span></span>

  <span data-ttu-id="12493-129">Central de segurança usa identificadores exclusivos de tooassign de enumeração de configuração comuns (CCE) para as regras de configuração.</span><span class="sxs-lookup"><span data-stu-id="12493-129">Security Center uses Common Configuration Enumeration (CCE) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="12493-130">Olá informações a seguir é fornecida nesta folha:</span><span class="sxs-lookup"><span data-stu-id="12493-130">hello following information is provided on this blade:</span></span>

  - <span data-ttu-id="12493-131">NOME -- o nome da regra</span><span class="sxs-lookup"><span data-stu-id="12493-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="12493-132">GRAVIDADE -- valor de gravidade da CCE de crítico, importante ou aviso</span><span class="sxs-lookup"><span data-stu-id="12493-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="12493-133">CCIED – Identificador exclusivo CCE para regra de saudação</span><span class="sxs-lookup"><span data-stu-id="12493-133">CCIED -- CCE unique identifier for hello rule</span></span>
  - <span data-ttu-id="12493-134">DESCRIÇÃO -- a descrição da regra</span><span class="sxs-lookup"><span data-stu-id="12493-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="12493-135">VULNERABILIDADE -- explicação da vulnerabilidade ou do risco se a regra não for aplicada</span><span class="sxs-lookup"><span data-stu-id="12493-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="12493-136">IMPACTO -- o impacto nos negócios quando a regra é aplicada</span><span class="sxs-lookup"><span data-stu-id="12493-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="12493-137">VALOR esperado – Valor esperado quando a Central de segurança analisa sua configuração de sistema operacional da VM em relação a regra de saudação</span><span class="sxs-lookup"><span data-stu-id="12493-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="12493-138">– REGRA regra operação usada pela Central de segurança durante a análise da configuração do sistema operacional da VM em relação a regra de saudação</span><span class="sxs-lookup"><span data-stu-id="12493-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="12493-139">VALOR real – O valor retornado após a análise da configuração do sistema operacional da VM em relação a regra de saudação</span><span class="sxs-lookup"><span data-stu-id="12493-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against hello rule</span></span>
  - <span data-ttu-id="12493-140">RESULTADO DA AVALIAÇÃO -- o resultado da análise: Aprovado, Falha</span><span class="sxs-lookup"><span data-stu-id="12493-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="12493-141">Consulte também</span><span class="sxs-lookup"><span data-stu-id="12493-141">See also</span></span>
<span data-ttu-id="12493-142">Este artigo lhe mostrou como tooimplement Olá Central de segurança recomendação "corrigir OS vulnerabilidades."</span><span class="sxs-lookup"><span data-stu-id="12493-142">This article showed you how tooimplement hello Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="12493-143">Você pode examinar o conjunto de saudação de regras de configuração [aqui](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="12493-143">You can review hello set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="12493-144">Central de segurança usa identificadores exclusivos de tooassign CCE (Common Configuration Enumeration) para as regras de configuração.</span><span class="sxs-lookup"><span data-stu-id="12493-144">Security Center uses CCE (Common Configuration Enumeration) tooassign unique identifiers for configuration rules.</span></span> <span data-ttu-id="12493-145">Visite Olá [CCE](https://nvd.nist.gov/cce/index.cfm) site para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="12493-145">Visit hello [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="12493-146">toolearn mais sobre o Centro de segurança, consulte Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="12493-146">toolearn more about Security Center, see hello following resources:</span></span>

* <span data-ttu-id="12493-147">[Plataformas com suporte na Central de Segurança do Azure](security-center-os-coverage.md) – fornece uma lista de VMs Windows e Linux com suporte.</span><span class="sxs-lookup"><span data-stu-id="12493-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="12493-148">[Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) -Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="12493-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="12493-149">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="12493-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="12493-150">[Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) -Saiba como toomonitor Olá a integridade de seus recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="12493-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="12493-151">[Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) -Saiba como alertas de toosecurity toomanage e responder.</span><span class="sxs-lookup"><span data-stu-id="12493-151">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="12493-152">[Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) -Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.</span><span class="sxs-lookup"><span data-stu-id="12493-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="12493-153">[Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) -perguntas frequentes sobre como usar o serviço de saudação de localizar.</span><span class="sxs-lookup"><span data-stu-id="12493-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="12493-154">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/): encontre postagens no blog sobre conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="12493-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
