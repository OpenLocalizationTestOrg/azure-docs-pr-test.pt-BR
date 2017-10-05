---
title: "Corrigir as vulnerabilidades do sistema operacional na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento mostra como implementar a recomendação da Central de Segurança do Azure para **Corrigir as vulnerabilidades do sistema operacional**."
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
ms.openlocfilehash: e6b251d5b97c57b3b6f79d14e53fbed5ca37ecb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a><span data-ttu-id="bb066-103">Corrigir as vulnerabilidades do sistema operacional na Central de Segurança do Azure</span><span class="sxs-lookup"><span data-stu-id="bb066-103">Remediate OS vulnerabilities in Azure Security Center</span></span>
<span data-ttu-id="bb066-104">Diariamente, a Central de Segurança do Azure analisa as configurações do sistema operacional (SO) da sua máquina virtual (VM) que podem tornar a VM mais vulnerável a ataques e recomenda as alterações de configuração para corrigir essas vulnerabilidades.</span><span class="sxs-lookup"><span data-stu-id="bb066-104">Azure Security Center analyzes daily your virtual machine (VM) operating system (OS) for configurations that could make the VM more vulnerable to attack and recommends configuration changes to address these vulnerabilities.</span></span> <span data-ttu-id="bb066-105">A Central de Segurança recomenda que você resolva as vulnerabilidades quando a configuração do SO da VM não seguir as regras de configuração recomendadas.</span><span class="sxs-lookup"><span data-stu-id="bb066-105">Security Center recommends that you resolve vulnerabilities when your VM’s OS configuration does not match the recommended configuration rules.</span></span>

> [!NOTE]
> <span data-ttu-id="bb066-106">Para obter mais informações sobre configurações específicas que estão sendo monitoradas, consulte a [lista de regras de configuração recomendadas](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="bb066-106">For more information on the specific configurations being monitored, see the [list of recommended configuration rules](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="bb066-107">Implementar a recomendação</span><span class="sxs-lookup"><span data-stu-id="bb066-107">Implement the recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="bb066-108">Este documento apresenta o serviço usando uma implantação de exemplo.</span><span class="sxs-lookup"><span data-stu-id="bb066-108">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="bb066-109">Este documento não é um guia passo a passo.</span><span class="sxs-lookup"><span data-stu-id="bb066-109">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="bb066-110">Na folha **Recomendações**, selecione **Corrigir vulnerabilidades do SO**.</span><span class="sxs-lookup"><span data-stu-id="bb066-110">In the **Recommendations** blade, select **Remediate OS vulnerabilities**.</span></span>
   <span data-ttu-id="bb066-111">![Corrigir as vulnerabilidades do sistema operacional][1]</span><span class="sxs-lookup"><span data-stu-id="bb066-111">![Remediate OS vulnerabilities][1]</span></span>

    <span data-ttu-id="bb066-112">A folha **Corrigir vulnerabilidades do SO** abre e lista as VMs que tenham configurações de SO que não seguem as regras de configuração recomendadas.</span><span class="sxs-lookup"><span data-stu-id="bb066-112">The **Remediate OS vulnerabilities** blade opens and lists your VMs with OS configurations that do not match the recommended configuration rules.</span></span>  <span data-ttu-id="bb066-113">Para cada VM, a folha identifica:</span><span class="sxs-lookup"><span data-stu-id="bb066-113">For each VM, the blade identifies:</span></span>

   * <span data-ttu-id="bb066-114">**REGRAS COM FALHAS** -- o número de regras de configuração que o SO da VM não segue.</span><span class="sxs-lookup"><span data-stu-id="bb066-114">**FAILED RULES** -- The number of rules that the VM's OS configuration failed.</span></span>
   * <span data-ttu-id="bb066-115">**HORA DA ÚLTIMA VERIFICAÇÃO** -- a data e a hora em que a Central de Segurança verificou pela última vez a configuração do SO da VM.</span><span class="sxs-lookup"><span data-stu-id="bb066-115">**LAST SCAN TIME** -- The date and time that Security Center last scanned the VM’s OS configuration.</span></span>
   * <span data-ttu-id="bb066-116">**ESTADO** --- o estado atual da vulnerabilidade:</span><span class="sxs-lookup"><span data-stu-id="bb066-116">**STATE** -- The current state of the vulnerability:</span></span>

     * <span data-ttu-id="bb066-117">Aberta: a vulnerabilidade ainda não foi corrigida</span><span class="sxs-lookup"><span data-stu-id="bb066-117">Open: The vulnerability has not been addressed yet</span></span>
     * <span data-ttu-id="bb066-118">Em andamento: a vulnerabilidade está sendo corrigida; não é exigido que você realize nenhuma ação</span><span class="sxs-lookup"><span data-stu-id="bb066-118">In Progress: The vulnerability is currently being applied, no action is required by you</span></span>
     * <span data-ttu-id="bb066-119">Resolvida: a vulnerabilidade já foi corrigida (quando o problema for resolvido, a entrada será esmaecida)</span><span class="sxs-lookup"><span data-stu-id="bb066-119">Resolved: The vulnerability was already addressed (when the issue has been resolved, the entry is grayed out)</span></span>
   * <span data-ttu-id="bb066-120">**GRAVIDADE** -- Todas as vulnerabilidades são definidas com uma gravidade Baixa, o que significa que a vulnerabilidade deve ser corrigida, mas não exige atenção imediata.</span><span class="sxs-lookup"><span data-stu-id="bb066-120">**SEVERITY** -- All vulnerabilities are set to a severity of Low, meaning a vulnerability should be addressed but does not require immediate attention.</span></span>

2. <span data-ttu-id="bb066-121">Selecionar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bb066-121">Select a VM.</span></span> <span data-ttu-id="bb066-122">Uma folha dessa VM é aberta e exibe as regras que falharam.</span><span class="sxs-lookup"><span data-stu-id="bb066-122">A blade for that VM opens and displays the rules that have failed.</span></span>
   <span data-ttu-id="bb066-123">![Regras de configuração que falharam][2]</span><span class="sxs-lookup"><span data-stu-id="bb066-123">![Configuration rules that have failed][2]</span></span>

3. <span data-ttu-id="bb066-124">Selecione uma regra.</span><span class="sxs-lookup"><span data-stu-id="bb066-124">Select a rule.</span></span> <span data-ttu-id="bb066-125">Neste exemplo, você pode selecionar **A senha deve atender a requisitos de complexidade**.</span><span class="sxs-lookup"><span data-stu-id="bb066-125">In this example, lets select **Password must meet complexity requirements**.</span></span> <span data-ttu-id="bb066-126">Uma folha será aberta descrevendo a regra com falha e o impacto.</span><span class="sxs-lookup"><span data-stu-id="bb066-126">A blade opens describing the failed rule and the impact.</span></span> <span data-ttu-id="bb066-127">Examine os detalhes e considere como as configurações do sistema operacional são aplicadas.</span><span class="sxs-lookup"><span data-stu-id="bb066-127">Review the details and consider how operating system configurations are applied.</span></span>
  <span data-ttu-id="bb066-128">![Descrição da regra com falha][3]</span><span class="sxs-lookup"><span data-stu-id="bb066-128">![Description for the failed rule][3]</span></span>

  <span data-ttu-id="bb066-129">A Central de Segurança usa a Common Configuration Enumeration (CCE) para atribuir identificadores exclusivos para as regras de configuração.</span><span class="sxs-lookup"><span data-stu-id="bb066-129">Security Center uses Common Configuration Enumeration (CCE) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="bb066-130">As informações a seguir são fornecidas nessa folha:</span><span class="sxs-lookup"><span data-stu-id="bb066-130">The following information is provided on this blade:</span></span>

  - <span data-ttu-id="bb066-131">NOME -- o nome da regra</span><span class="sxs-lookup"><span data-stu-id="bb066-131">NAME -- Name of rule</span></span>
  - <span data-ttu-id="bb066-132">GRAVIDADE -- valor de gravidade da CCE de crítico, importante ou aviso</span><span class="sxs-lookup"><span data-stu-id="bb066-132">SEVERITY -- CCE severity value of critical, important, or warning</span></span>
  - <span data-ttu-id="bb066-133">CCIED -- identificador exclusivo da CCE para a regra</span><span class="sxs-lookup"><span data-stu-id="bb066-133">CCIED -- CCE unique identifier for the rule</span></span>
  - <span data-ttu-id="bb066-134">DESCRIÇÃO -- a descrição da regra</span><span class="sxs-lookup"><span data-stu-id="bb066-134">DESCRIPTION -- Description of rule</span></span>
  - <span data-ttu-id="bb066-135">VULNERABILIDADE -- explicação da vulnerabilidade ou do risco se a regra não for aplicada</span><span class="sxs-lookup"><span data-stu-id="bb066-135">VULNERABILITY -- Explanation of vulnerability or risk if rule is not applied</span></span>
  - <span data-ttu-id="bb066-136">IMPACTO -- o impacto nos negócios quando a regra é aplicada</span><span class="sxs-lookup"><span data-stu-id="bb066-136">IMPACT -- Business impact when rule is applied</span></span>
  - <span data-ttu-id="bb066-137">VALOR ESPERADO -- o valor esperado quando a Central de Segurança analisa a configuração do SO da VM em relação à regra</span><span class="sxs-lookup"><span data-stu-id="bb066-137">EXPECTED VALUE -- Value expected when Security Center analyzes your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="bb066-138">OPERAÇÃO DA REGRA -- a operação da regra usada pela Central de Segurança durante a análise da configuração do SO da VM em relação à regra</span><span class="sxs-lookup"><span data-stu-id="bb066-138">RULE OPERATION -- Rule operation used by Security Center during analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="bb066-139">VALOR REAL -- o valor retornado após a análise da configuração do SO da VM em relação à regra</span><span class="sxs-lookup"><span data-stu-id="bb066-139">ACTUAL VALUE -- Value returned after analysis of your VM OS configuration against the rule</span></span>
  - <span data-ttu-id="bb066-140">RESULTADO DA AVALIAÇÃO -- o resultado da análise: Aprovado, Falha</span><span class="sxs-lookup"><span data-stu-id="bb066-140">EVALUATION RESULT –- Result of analysis: Pass, Fail</span></span>

## <a name="see-also"></a><span data-ttu-id="bb066-141">Consulte também</span><span class="sxs-lookup"><span data-stu-id="bb066-141">See also</span></span>
<span data-ttu-id="bb066-142">Este artigo mostrou como implementar a recomendação da Central de Segurança para "Corrigir vulnerabilidades do sistema operacional".</span><span class="sxs-lookup"><span data-stu-id="bb066-142">This article showed you how to implement the Security Center recommendation "Remediate OS vulnerabilities."</span></span> <span data-ttu-id="bb066-143">Você pode conferir o conjunto de regras de configuração [aqui](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span><span class="sxs-lookup"><span data-stu-id="bb066-143">You can review the set of configuration rules [here](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).</span></span> <span data-ttu-id="bb066-144">A Central de Segurança usa a Common Configuration Enumeration (CCE) para atribuir identificadores exclusivos para as regras de configuração.</span><span class="sxs-lookup"><span data-stu-id="bb066-144">Security Center uses CCE (Common Configuration Enumeration) to assign unique identifiers for configuration rules.</span></span> <span data-ttu-id="bb066-145">Visite o site da [CCE](https://nvd.nist.gov/cce/index.cfm) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="bb066-145">Visit the [CCE](https://nvd.nist.gov/cce/index.cfm) site for more information.</span></span>

<span data-ttu-id="bb066-146">Para saber mais sobre a Central de Segurança, confira os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="bb066-146">To learn more about Security Center, see the following resources:</span></span>

* <span data-ttu-id="bb066-147">[Plataformas com suporte na Central de Segurança do Azure](security-center-os-coverage.md) – fornece uma lista de VMs Windows e Linux com suporte.</span><span class="sxs-lookup"><span data-stu-id="bb066-147">[Supported platforms in Azure Security Center](security-center-os-coverage.md) - Provides a list of supported Windows and Linux VMs.</span></span>
* <span data-ttu-id="bb066-148">[Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md): saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb066-148">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="bb066-149">[Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb066-149">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="bb066-150">[Monitoramento da integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md): saiba como monitorar a integridade dos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb066-150">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="bb066-151">[Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md): aprenda a gerenciar e responder aos alertas de segurança.</span><span class="sxs-lookup"><span data-stu-id="bb066-151">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="bb066-152">[Monitorando as soluções de parceiros com a Central de Segurança do Azure](security-center-partner-solutions.md) – saiba como monitorar o status de integridade de suas soluções de parceiros.</span><span class="sxs-lookup"><span data-stu-id="bb066-152">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) - Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="bb066-153">[Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md): encontre as perguntas frequentes sobre como usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="bb066-153">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="bb066-154">[Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/): encontre postagens no blog sobre conformidade e segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb066-154">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
