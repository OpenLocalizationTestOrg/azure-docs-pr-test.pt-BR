---
title: "Proteção de identidade do Active Directory de aaaAzure | Microsoft Docs"
description: "Saiba como Azure AD Identity Protection permite que você toolimit capacidade Olá tooexploit um invasor uma identidade comprometida ou dispositivo e toosecure uma identidade ou um dispositivo que era anteriormente conhecido ou suspeita toobe comprometido."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gerenciamento de aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="d349c-104">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="d349c-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="d349c-105">Proteção contra identidade Active Directory do Azure é um recurso de edição de saudação do Azure AD Premium P2 que permite que você:</span><span class="sxs-lookup"><span data-stu-id="d349c-105">Azure Active Directory Identity Protection is a feature of hello Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="d349c-106">Detectar possíveis vulnerabilidades que afetam as identidades da organização</span><span class="sxs-lookup"><span data-stu-id="d349c-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="d349c-107">Configurar respostas automatizadas toodetected suspeitas ações de identidades da organização tooyour relacionados</span><span class="sxs-lookup"><span data-stu-id="d349c-107">Configure automated responses toodetected suspicious actions that are related tooyour organization’s identities</span></span>  

- <span data-ttu-id="d349c-108">Investigar incidentes suspeitos e tomar a ação apropriada tooresolve-los</span><span class="sxs-lookup"><span data-stu-id="d349c-108">Investigate suspicious incidents and take appropriate action tooresolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="d349c-109">Introdução</span><span class="sxs-lookup"><span data-stu-id="d349c-109">Getting started</span></span>

<span data-ttu-id="d349c-110">A Microsoft protege identidades baseadas em nuvem há mais de uma década.</span><span class="sxs-lookup"><span data-stu-id="d349c-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="d349c-111">Com o Azure Active Directory Identity Protection em seu ambiente, você pode usar Olá mesmos sistemas de proteção Microsoft usa toosecure identidades.</span><span class="sxs-lookup"><span data-stu-id="d349c-111">With Azure Active Directory Identity Protection, in your environment, you can use hello same protection systems Microsoft uses toosecure identities.</span></span>

<span data-ttu-id="d349c-112">maioria de saudação de levar violações de segurança colocar quando os invasores obterem o ambiente de tooan acesso pelo roubo de identidade do usuário.</span><span class="sxs-lookup"><span data-stu-id="d349c-112">hello vast majority of security breaches take place when attackers gain access tooan environment by stealing a user’s identity.</span></span> <span data-ttu-id="d349c-113">Ao longo de anos de hello, os invasores tornaram cada vez mais eficazes, aproveitando as violações de terceiros e uso de ataques de phishing sofisticados.</span><span class="sxs-lookup"><span data-stu-id="d349c-113">Over hello years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="d349c-114">Assim que um invasor obtiver acesso a contas de usuário com privilégios baixos tooeven, é relativamente fácil tooimportant toogain acessar recursos da empresa por meio de movimentação lateral.</span><span class="sxs-lookup"><span data-stu-id="d349c-114">As soon as an attacker gains access tooeven low privileged user accounts, it is relatively easy for them toogain access tooimportant company resources through lateral movement.</span></span>

<span data-ttu-id="d349c-115">Como consequência, você precisa:</span><span class="sxs-lookup"><span data-stu-id="d349c-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="d349c-116">Proteger todas as identidades, independentemente do nível de privilégio</span><span class="sxs-lookup"><span data-stu-id="d349c-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="d349c-117">Agir proativamente para evitar o uso de identidades comprometidas</span><span class="sxs-lookup"><span data-stu-id="d349c-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="d349c-118">Descobrir identidades comprometidas não é uma tarefa fácil.</span><span class="sxs-lookup"><span data-stu-id="d349c-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="d349c-119">Active Directory do Azure usa algoritmos de aprendizado de máquina adaptável e anomalias de toodetect heurística e incidentes suspeitos que indicam potencialmente comprometidos identidades.</span><span class="sxs-lookup"><span data-stu-id="d349c-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="d349c-120">Usando esses dados, proteção de identidade gera relatórios e alertas que permitem que você tooevaluate Olá detectou problemas e tomar ações de correção ou atenuação apropriada.</span><span class="sxs-lookup"><span data-stu-id="d349c-120">Using this data, Identity Protection generates reports and alerts that enable you tooevaluate hello detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="d349c-121">O Azure Active Directory Identity Protection é mais do que apenas uma ferramenta de monitoramento e criação de relatórios.</span><span class="sxs-lookup"><span data-stu-id="d349c-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="d349c-122">tooprotect identidades da sua organização, você pode configurar políticas baseadas em risco que respondem automaticamente toodetected problemas quando um nível de risco especificado for atingido.</span><span class="sxs-lookup"><span data-stu-id="d349c-122">tooprotect your organization's identities, you can configure risk-based policies that automatically respond toodetected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="d349c-123">Essas políticas, além de tooother condicional acessar controles fornecidos pelo Active Directory do Azure e o EMS, pode bloquear automaticamente ou iniciar ações de correção adaptável, inclusive redefinições de senha e a imposição de autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="d349c-123">These policies, in addition tooother conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="d349c-124">Recursos do Identity Protection</span><span class="sxs-lookup"><span data-stu-id="d349c-124">Identity Protection capabilities</span></span>

<span data-ttu-id="d349c-125">**Detecção de vulnerabilidades e contas de risco:**</span><span class="sxs-lookup"><span data-stu-id="d349c-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="d349c-126">Fornecendo recomendações personalizadas tooimprove postura de segurança geral, realçando vulnerabilidades</span><span class="sxs-lookup"><span data-stu-id="d349c-126">Providing custom recommendations tooimprove overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="d349c-127">Calcular os níveis de risco de entrada</span><span class="sxs-lookup"><span data-stu-id="d349c-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="d349c-128">Calcular os níveis de risco do usuário</span><span class="sxs-lookup"><span data-stu-id="d349c-128">Calculating user risk levels</span></span>


<span data-ttu-id="d349c-129">**Investigação dos eventos de risco:**</span><span class="sxs-lookup"><span data-stu-id="d349c-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="d349c-130">Enviar notificações para eventos de risco</span><span class="sxs-lookup"><span data-stu-id="d349c-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="d349c-131">Investigar os eventos de risco usando informações relevantes e contextuais</span><span class="sxs-lookup"><span data-stu-id="d349c-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="d349c-132">Fornecendo tootrack investigações de fluxos de trabalho básicos</span><span class="sxs-lookup"><span data-stu-id="d349c-132">Providing basic workflows tootrack investigations</span></span>
* <span data-ttu-id="d349c-133">Fornecer acesso fácil tooremediation ações, como a redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="d349c-133">Providing easy access tooremediation actions such as password reset</span></span>

<span data-ttu-id="d349c-134">**Políticas de acesso condicional baseadas em risco:**</span><span class="sxs-lookup"><span data-stu-id="d349c-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="d349c-135">Diretiva toomitigate arriscadas entradas bloqueando entradas ou a necessidade de desafios de autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="d349c-135">Policy toomitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="d349c-136">Diretiva tooblock ou contas de usuário de arriscados segura</span><span class="sxs-lookup"><span data-stu-id="d349c-136">Policy tooblock or secure risky user accounts</span></span>
* <span data-ttu-id="d349c-137">Diretiva toorequire usuários tooregister para autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="d349c-137">Policy toorequire users tooregister for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="d349c-138">Funções da proteção de identidade</span><span class="sxs-lookup"><span data-stu-id="d349c-138">Identity Protection roles</span></span>

<span data-ttu-id="d349c-139">atividades de gerenciamento tooload saldo Olá em torno de sua implementação de proteção de identidade, você pode atribuir várias funções.</span><span class="sxs-lookup"><span data-stu-id="d349c-139">tooload balance hello management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="d349c-140">O Azure AD Identity Protection dá suporte a três funções do diretório:</span><span class="sxs-lookup"><span data-stu-id="d349c-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="d349c-141">Função</span><span class="sxs-lookup"><span data-stu-id="d349c-141">Role</span></span>                         | <span data-ttu-id="d349c-142">O que ele pode fazer</span><span class="sxs-lookup"><span data-stu-id="d349c-142">Can do</span></span>                          | <span data-ttu-id="d349c-143">O que não pode fazer</span><span class="sxs-lookup"><span data-stu-id="d349c-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="d349c-144">Administrador global</span><span class="sxs-lookup"><span data-stu-id="d349c-144">Global administrator</span></span>         | <span data-ttu-id="d349c-145">Acesso completo tooIdentity proteção integrada de proteção de identidade</span><span class="sxs-lookup"><span data-stu-id="d349c-145">Full access tooIdentity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="d349c-146">Administrador de segurança</span><span class="sxs-lookup"><span data-stu-id="d349c-146">Security administrator</span></span>       | <span data-ttu-id="d349c-147">Acesso completo tooIdentity proteção</span><span class="sxs-lookup"><span data-stu-id="d349c-147">Full access tooIdentity Protection</span></span> | <span data-ttu-id="d349c-148">Proteção de Identidade integrada, redefinir senhas para um usuário</span><span class="sxs-lookup"><span data-stu-id="d349c-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="d349c-149">Leitor de segurança</span><span class="sxs-lookup"><span data-stu-id="d349c-149">Security reader</span></span>              | <span data-ttu-id="d349c-150">Acesso somente leitura tooIdentity proteção</span><span class="sxs-lookup"><span data-stu-id="d349c-150">Ready-only access tooIdentity Protection</span></span> | <span data-ttu-id="d349c-151">Integrar Proteção de Identidade, corrigir usuários, configurar políticas, redefinir senhas</span><span class="sxs-lookup"><span data-stu-id="d349c-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="d349c-152">Para saber mais detalhes, consulte [Atribuindo funções de administrador no Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d349c-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="d349c-153">Detecção</span><span class="sxs-lookup"><span data-stu-id="d349c-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="d349c-154">Vulnerabilidades</span><span class="sxs-lookup"><span data-stu-id="d349c-154">Vulnerabilities</span></span>

<span data-ttu-id="d349c-155">O Azure Active Directory Identity Protection analisa sua configuração e detecta vulnerabilidades que podem ter impacto nas identidades do usuário.</span><span class="sxs-lookup"><span data-stu-id="d349c-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="d349c-156">Para saber mais, confira [Vulnerabilidades detectadas pelo Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="d349c-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="d349c-157">Eventos de risco</span><span class="sxs-lookup"><span data-stu-id="d349c-157">Risk events</span></span>

<span data-ttu-id="d349c-158">Active Directory do Azure usa algoritmos e heurística toodetect suspeitas ações de identidades do usuário relacionadas tooyour de aprendizado de máquina adaptável.</span><span class="sxs-lookup"><span data-stu-id="d349c-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user's identities.</span></span> <span data-ttu-id="d349c-159">sistema de saudação cria um registro para cada ação suspeita detectada.</span><span class="sxs-lookup"><span data-stu-id="d349c-159">hello system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="d349c-160">Esses registros também são conhecidos como eventos de risco.</span><span class="sxs-lookup"><span data-stu-id="d349c-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="d349c-161">Para obter mais detalhes, veja [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="d349c-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="d349c-162">Investigação</span><span class="sxs-lookup"><span data-stu-id="d349c-162">Investigation</span></span>
<span data-ttu-id="d349c-163">Sua jornada com proteção de identidade normalmente inicia com o painel de proteção de identidade hello.</span><span class="sxs-lookup"><span data-stu-id="d349c-163">Your journey through Identity Protection typically starts with hello Identity Protection dashboard.</span></span>

<span data-ttu-id="d349c-164">![Correção](./media/active-directory-identityprotection/1000.png "Correção")</span><span class="sxs-lookup"><span data-stu-id="d349c-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="d349c-165">painel Olá fornece acesso para:</span><span class="sxs-lookup"><span data-stu-id="d349c-165">hello dashboard gives you access to:</span></span>

* <span data-ttu-id="d349c-166">Relatórios, como **Usuários sinalizados por riscos**, **Eventos de risco** e **Vulnerabilidades**</span><span class="sxs-lookup"><span data-stu-id="d349c-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="d349c-167">As configurações como a configuração de saudação do seu **políticas de segurança**, **notificações** e **registro de autenticação multifator**</span><span class="sxs-lookup"><span data-stu-id="d349c-167">Settings such as hello configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="d349c-168">Normalmente é o ponto de partida para investigação, que é o processo de saudação de revisão Olá atividades, logs e outras informações relevantes tooa relacionado toodecide de evento de risco se são necessárias etapas de correção ou de redução, e como a identidade de saudação foi comprometido e entender como Olá comprometidos identidade foi usada.</span><span class="sxs-lookup"><span data-stu-id="d349c-168">It is typically your starting point for investigation, which is hello process of reviewing hello activities, logs, and other relevant information related tooa risk event toodecide whether remediation or mitigation steps are necessary,  and how hello identity was compromised, and understand how hello compromised identity was used.</span></span>

<span data-ttu-id="d349c-169">É possível vincular sua toohello de atividades de investigação [notificações](active-directory-identityprotection-notifications.md) proteção do Azure Active Directory envia por email.</span><span class="sxs-lookup"><span data-stu-id="d349c-169">You can tie your investigation activities toohello [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="d349c-170">Olá seções a seguir fornecem mais detalhes e etapas Olá investigação tooan relacionados.</span><span class="sxs-lookup"><span data-stu-id="d349c-170">hello following sections provide you with more details and hello steps that are related tooan investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="d349c-171">Entradas de risco</span><span class="sxs-lookup"><span data-stu-id="d349c-171">Risky sign-ins</span></span>

<span data-ttu-id="d349c-172">O Azure Active Directory detecta [tipos de evento de risco](active-directory-reporting-risk-events.md#risk-event-types) em tempo real e offline.</span><span class="sxs-lookup"><span data-stu-id="d349c-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="d349c-173">Cada evento de risco que foi detectado para uma entrada de um usuário contribui tooa conceito lógico chamado entrar arriscado.</span><span class="sxs-lookup"><span data-stu-id="d349c-173">Each risk event that has been detected for a sign-in of a user contributes tooa logical concept called risky sign-in.</span></span> <span data-ttu-id="d349c-174">Uma entrada arriscado é um indicador para uma tentativa de logon que não pode ter sido realizada pelo proprietário da saudação legítimo de uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="d349c-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by hello legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="d349c-175">Nível de risco de entrada</span><span class="sxs-lookup"><span data-stu-id="d349c-175">Sign-in risk level</span></span>

<span data-ttu-id="d349c-176">Um nível de risco de entrada é uma indicação (alto, médio ou baixo) de probabilidade Olá que uma tentativa de logon não foi executada pelo proprietário da saudação legítimo de uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="d349c-176">A sign-in risk level is an indication (High, Medium, or Low) of hello likelihood that a sign-in attempt was not performed by hello legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="d349c-177">Mitigação de eventos de risco de entrada</span><span class="sxs-lookup"><span data-stu-id="d349c-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="d349c-178">Uma redução é uma ação toolimit Olá capacidade um invasor tooexploit uma identidade comprometida ou dispositivo sem estado de restauração Olá identidade ou dispositivo tooa seguro.</span><span class="sxs-lookup"><span data-stu-id="d349c-178">A mitigation is an action toolimit hello ability of an attacker tooexploit a compromised identity or device without restoring hello identity or device tooa safe state.</span></span> <span data-ttu-id="d349c-179">Uma redução não resolver anterior eventos de entrada risco associados à identidade hello ou dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d349c-179">A mitigation does not resolve previous sign-in risk events associated with hello identity or device.</span></span>

<span data-ttu-id="d349c-180">toomitigate arriscados entradas automaticamente, você pode configurar o risco de entrada policicies de segurança.</span><span class="sxs-lookup"><span data-stu-id="d349c-180">toomitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="d349c-181">Usando essas diretivas, considere o nível de risco de saudação do usuário hello ou Olá entrar tooblock entradas arriscadas ou exigir autenticação multifator do hello usuário tooperform.</span><span class="sxs-lookup"><span data-stu-id="d349c-181">Using these policies, you consider hello risk level of hello user or hello sign-in tooblock risky sign-ins or require hello user tooperform multi-factor authentication.</span></span> <span data-ttu-id="d349c-182">Essas ações podem impedir que um invasor explorar um dano de toocause roubo de identidade e podem fornecer uma identidade de Olá de toosecure algum tempo.</span><span class="sxs-lookup"><span data-stu-id="d349c-182">These actions may prevent an attacker from exploiting a stolen identity toocause damage, and may give you some time toosecure hello identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="d349c-183">Política de segurança de risco de entrada</span><span class="sxs-lookup"><span data-stu-id="d349c-183">Sign-in risk security policy</span></span>
<span data-ttu-id="d349c-184">Uma política de risco de entrada é uma política de acesso condicional que é avaliada Olá risco tooa sign-in específico e aplica atenuações com base em regras e condições predefinidas.</span><span class="sxs-lookup"><span data-stu-id="d349c-184">A sign-in risk policy is a conditional access policy that evaluates hello risk tooa specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="d349c-185">![Política de risco de entrada](./media/active-directory-identityprotection/1014.png "Política de risco de entrada")</span><span class="sxs-lookup"><span data-stu-id="d349c-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="d349c-186">Azure AD Identity Protection ajuda você a gerenciar a mitigação de saudação de entradas arriscadas, permitindo que você:</span><span class="sxs-lookup"><span data-stu-id="d349c-186">Azure AD Identity Protection helps you manage hello mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="d349c-187">Definir Olá usuários e grupos Olá política aplica-se a:</span><span class="sxs-lookup"><span data-stu-id="d349c-187">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="d349c-188">![Política de risco de entrada](./media/active-directory-identityprotection/1015.png "Política de risco de entrada")</span><span class="sxs-lookup"><span data-stu-id="d349c-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="d349c-189">Defina Olá entrar risco nível limite (baixa, média ou alta) que dispara a política de saudação:</span><span class="sxs-lookup"><span data-stu-id="d349c-189">Set hello sign-in risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="d349c-190">![Política de risco de entrada](./media/active-directory-identityprotection/1016.png "Política de risco de entrada")</span><span class="sxs-lookup"><span data-stu-id="d349c-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="d349c-191">Conjunto Olá controles toobe imposta quando a política de saudação dispara:</span><span class="sxs-lookup"><span data-stu-id="d349c-191">Set hello controls toobe enforced when hello policy triggers:</span></span>  

    <span data-ttu-id="d349c-192">![Política de risco de entrada](./media/active-directory-identityprotection/1017.png "Política de risco de entrada")</span><span class="sxs-lookup"><span data-stu-id="d349c-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="d349c-193">Alternar estado Olá da política:</span><span class="sxs-lookup"><span data-stu-id="d349c-193">Switch hello state of your policy:</span></span>

    <span data-ttu-id="d349c-194">![Registro de MFA](./media/active-directory-identityprotection/403.png "Registro de MFA")</span><span class="sxs-lookup"><span data-stu-id="d349c-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="d349c-195">Revisar e avaliar o impacto de saudação de uma alteração antes de ativá-lo:</span><span class="sxs-lookup"><span data-stu-id="d349c-195">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="d349c-196">![Política de risco de entrada](./media/active-directory-identityprotection/1018.png "Política de risco de entrada")</span><span class="sxs-lookup"><span data-stu-id="d349c-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-tooknow"></a><span data-ttu-id="d349c-197">O que você precisa tooknow</span><span class="sxs-lookup"><span data-stu-id="d349c-197">What you need tooknow</span></span>
<span data-ttu-id="d349c-198">Você pode configurar uma autenticação multifator do risco de entrada segurança política toorequire:</span><span class="sxs-lookup"><span data-stu-id="d349c-198">You can configure a sign-in risk security policy toorequire multi-factor authentication:</span></span>

<span data-ttu-id="d349c-199">![Política de risco de entrada](./media/active-directory-identityprotection/1017.png "Política de risco de entrada")</span><span class="sxs-lookup"><span data-stu-id="d349c-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="d349c-200">No entanto, por motivos de segurança, essa configuração só funciona para usuários que já foram registrados na autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="d349c-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="d349c-201">Se a autenticação de vários fatores de toorequire Olá condição é atendida para um usuário que ainda não foi registrado para autenticação multifator, usuário Olá será bloqueado.</span><span class="sxs-lookup"><span data-stu-id="d349c-201">If hello condition toorequire multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, hello user is blocked.</span></span>

<span data-ttu-id="d349c-202">Como prática recomendada, se você quiser toorequire multi-factor authentication arriscadas entradas, você deve:</span><span class="sxs-lookup"><span data-stu-id="d349c-202">As a best practice, if you want toorequire multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="d349c-203">Habilitar Olá [política de registro de autenticação multifator](#multi-factor-authentication-registration-policy) para Olá usuários afetados.</span><span class="sxs-lookup"><span data-stu-id="d349c-203">Enable hello [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for hello affected users.</span></span>
2. <span data-ttu-id="d349c-204">Exigir Olá afetados toologin de usuários em uma sessão não pode ser arriscado tooperform um registro MFA</span><span class="sxs-lookup"><span data-stu-id="d349c-204">Require hello affected users toologin in a non-risky session tooperform a MFA registration</span></span>

<span data-ttu-id="d349c-205">A conclusão dessas etapas faz com que a autenticação multifator seja exigida em caso de entrada de risco.</span><span class="sxs-lookup"><span data-stu-id="d349c-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="d349c-206">Práticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="d349c-206">Best practices</span></span>
<span data-ttu-id="d349c-207">Escolhendo um **alta** limite reduz o número de saudação de vezes que uma política é disparada e minimiza Olá impacto toousers.</span><span class="sxs-lookup"><span data-stu-id="d349c-207">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>  

<span data-ttu-id="d349c-208">No entanto, ele exclui **baixo** e **médio** sinalizado como entradas para o risco da política de saudação, que não pode impedir que um invasor explorar uma identidade comprometida.</span><span class="sxs-lookup"><span data-stu-id="d349c-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from hello policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="d349c-209">Quando a configuração Olá política,</span><span class="sxs-lookup"><span data-stu-id="d349c-209">When setting hello policy,</span></span>

* <span data-ttu-id="d349c-210">exclua os usuários que não tem / não podem ter a autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="d349c-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="d349c-211">Exclua os usuários em locais onde habilitando Olá política não é prático (por exemplo, nenhum toohelpdesk de acesso)</span><span class="sxs-lookup"><span data-stu-id="d349c-211">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="d349c-212">Exclua os usuários que são provavelmente toogenerate muitos falsos positivos (desenvolvedores, analistas de segurança)</span><span class="sxs-lookup"><span data-stu-id="d349c-212">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="d349c-213">use um limite **Alto** durante a distribuição inicial de política ou se você precisar minimizar os desafios encontrados pelos usuários finais.</span><span class="sxs-lookup"><span data-stu-id="d349c-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="d349c-214">Use um limite **Baixo** se sua organização exigir uma segurança maior.</span><span class="sxs-lookup"><span data-stu-id="d349c-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="d349c-215">Selecionar um limite **Baixo** apresenta desafios de entrada do usuário adicionais, porém representa uma segurança maior.</span><span class="sxs-lookup"><span data-stu-id="d349c-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="d349c-216">Olá recomendado padrão para a maioria das organizações é tooconfigure uma regra para um **médio** limite toostrike um equilíbrio entre segurança e facilidade de uso.</span><span class="sxs-lookup"><span data-stu-id="d349c-216">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="d349c-217">política de risco de entrada Hello é:</span><span class="sxs-lookup"><span data-stu-id="d349c-217">hello sign-in risk policy is:</span></span>

* <span data-ttu-id="d349c-218">Tráfego de navegador tooall aplicados e logons que usam autenticação moderna.</span><span class="sxs-lookup"><span data-stu-id="d349c-218">Applied tooall browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="d349c-219">Tooapplications não aplicada usando protocolos de segurança mais antigos, desabilitando o ponto de extremidade do WS-Trust de saudação IDP Olá federado, como o AD FS.</span><span class="sxs-lookup"><span data-stu-id="d349c-219">Not applied tooapplications using older security protocols by disabling hello WS-Trust endpoint at hello federated IDP, such as ADFS.</span></span>

<span data-ttu-id="d349c-220">Olá **eventos de risco** página no console de proteção de identidade Olá lista todos os eventos:</span><span class="sxs-lookup"><span data-stu-id="d349c-220">hello **Risk Events** page in hello Identity Protection console lists all events:</span></span>

* <span data-ttu-id="d349c-221">aos quais essa política se aplica</span><span class="sxs-lookup"><span data-stu-id="d349c-221">This policy was applied to</span></span>
* <span data-ttu-id="d349c-222">Você pode examinar a atividade de saudação e determinar se a ação de saudação era apropriada ou não</span><span class="sxs-lookup"><span data-stu-id="d349c-222">You can review hello activity and determine whether hello action was appropriate or not</span></span>

<span data-ttu-id="d349c-223">Para obter uma visão geral de saudação relacionadas a experiência do usuário, consulte:</span><span class="sxs-lookup"><span data-stu-id="d349c-223">For an overview of hello related user experience, see:</span></span>

* [<span data-ttu-id="d349c-224">Recuperação de entrada arriscada</span><span class="sxs-lookup"><span data-stu-id="d349c-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="d349c-225">Entrada arriscada bloqueada</span><span class="sxs-lookup"><span data-stu-id="d349c-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="d349c-226">Experiências de entrada com o Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="d349c-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="d349c-227">**caixa de diálogo de configuração relacionados de saudação tooopen**:</span><span class="sxs-lookup"><span data-stu-id="d349c-227">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="d349c-228">Em Olá **Azure AD Identity Protection** folha em Olá **configurar** seção, clique em **risco política**.</span><span class="sxs-lookup"><span data-stu-id="d349c-228">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="d349c-229">![Política do usuário ridk](./media/active-directory-identityprotection/1014.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="d349c-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="d349c-230">Usuários sinalizados por risco</span><span class="sxs-lookup"><span data-stu-id="d349c-230">Users flagged for risk</span></span>

<span data-ttu-id="d349c-231">Todos os ativos [eventos de risco](active-directory-identity-protection-risk-events.md) que foram detectados pelo Azure Active Directory para um usuário contribuir tooa conceito lógico chamado risco do usuário.</span><span class="sxs-lookup"><span data-stu-id="d349c-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute tooa logical concept called user risk.</span></span> <span data-ttu-id="d349c-232">Um usuários sinalizado como de risco é um indicador de que uma conta de usuário pode ter sido comprometida.</span><span class="sxs-lookup"><span data-stu-id="d349c-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Usuários sinalizados por risco](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="d349c-234">Nível de risco do usuário</span><span class="sxs-lookup"><span data-stu-id="d349c-234">User risk level</span></span>

<span data-ttu-id="d349c-235">Um nível de risco do usuário é uma indicação (alto, médio ou baixo) de probabilidade Olá Olá a identidade de usuário foi comprometida.</span><span class="sxs-lookup"><span data-stu-id="d349c-235">A user risk level is an indication (High, Medium, or Low) of hello likelihood that hello user’s identity has been compromised.</span></span> <span data-ttu-id="d349c-236">Ele é calculado com base em eventos de risco do usuário Olá que estão associados com a identidade do usuário.</span><span class="sxs-lookup"><span data-stu-id="d349c-236">It is calculated based on hello user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="d349c-237">Olá status de um evento de risco é **Active** ou **fechado**.</span><span class="sxs-lookup"><span data-stu-id="d349c-237">hello status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="d349c-238">Somente eventos de risco **Active** contribuem cálculo do nível de risco do usuário toohello.</span><span class="sxs-lookup"><span data-stu-id="d349c-238">Only risk events that are **Active** contribute toohello user risk level calculation.</span></span>

<span data-ttu-id="d349c-239">nível de risco do usuário Olá é calculada usando Olá entradas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d349c-239">hello user risk level is calculated using hello following inputs:</span></span>

* <span data-ttu-id="d349c-240">Eventos de risco ativo afetar o usuário Olá</span><span class="sxs-lookup"><span data-stu-id="d349c-240">Active risk events impacting hello user</span></span>
* <span data-ttu-id="d349c-241">Nível de risco desses eventos</span><span class="sxs-lookup"><span data-stu-id="d349c-241">Risk level of these events</span></span>
* <span data-ttu-id="d349c-242">Se foram tomadas ações de correção</span><span class="sxs-lookup"><span data-stu-id="d349c-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="d349c-243">![Riscos de usuário](./media/active-directory-identityprotection/1031.png "Riscos de usuário")</span><span class="sxs-lookup"><span data-stu-id="d349c-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="d349c-244">Você pode usar o hello usuário risco níveis toocreate políticas de acesso condicional que impedir que usuários arriscados entrar, ou forçá-los toosecurely alterar sua senha.</span><span class="sxs-lookup"><span data-stu-id="d349c-244">You can use hello user risk levels toocreate conditional access policies that block risky users from signing in, or force them toosecurely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="d349c-245">Fechar eventos de risco manualmente</span><span class="sxs-lookup"><span data-stu-id="d349c-245">Closing risk events manually</span></span>

<span data-ttu-id="d349c-246">Na maioria dos casos, você coloca as ações de correção, como eventos de risco fechar tooautomatically de redefinição de uma senha segura.</span><span class="sxs-lookup"><span data-stu-id="d349c-246">In most cases, you will take remediation actions such as a secure password reset tooautomatically close risk events.</span></span> <span data-ttu-id="d349c-247">No entanto, isso nem sempre é possível.</span><span class="sxs-lookup"><span data-stu-id="d349c-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="d349c-248">Isso acontece, por exemplo, Olá, quando:</span><span class="sxs-lookup"><span data-stu-id="d349c-248">This is, for example, hello case, when:</span></span>

* <span data-ttu-id="d349c-249">um usuário com eventos de risco ativo foi excluído</span><span class="sxs-lookup"><span data-stu-id="d349c-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="d349c-250">Uma investigação revela que um evento de risco relatado tem sido executar por usuário legítimo Olá</span><span class="sxs-lookup"><span data-stu-id="d349c-250">An investigation reveals that a reported risk event has been perform by hello legitimate user</span></span>

<span data-ttu-id="d349c-251">Como eventos de risco que são **Active** contribuem toohello cálculo de risco de usuário, você pode ter toomanually diminuir um nível de risco fechando os eventos de risco manualmente.</span><span class="sxs-lookup"><span data-stu-id="d349c-251">Because risk events that are **Active** contribute toohello user risk calculation, you may have toomanually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="d349c-252">Durante o curso de saudação da investigação, você pode escolher tootake, qualquer um dos status de saudação de toochange ações de um evento de risco:</span><span class="sxs-lookup"><span data-stu-id="d349c-252">During hello course of investigation, you can choose tootake any of these actions toochange hello status of a risk event:</span></span>

<span data-ttu-id="d349c-253">![Ações](./media/active-directory-identityprotection/34.png "Ações")</span><span class="sxs-lookup"><span data-stu-id="d349c-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="d349c-254">**Resolver** - se após investigar um evento de risco, você fez uma ação de correção apropriada sem proteção de identidade, e você achar que eventos de risco Olá devem ser considerado fechado, o evento de saudação marcar como resolvido.</span><span class="sxs-lookup"><span data-stu-id="d349c-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that hello risk event should be considered closed, mark hello event as Resolved.</span></span> <span data-ttu-id="d349c-255">Eventos resolvidos definirá tooClosed de status do evento de risco hello e eventos de risco Olá não contribuirá toouser risco.</span><span class="sxs-lookup"><span data-stu-id="d349c-255">Resolved events will set hello risk event’s status tooClosed and hello risk event will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="d349c-256">**Marcar como falso positivo** - Em alguns casos, você pode investigar um evento de risco e descobrir que ele foi sinalizado incorretamente como uma situação arriscada.</span><span class="sxs-lookup"><span data-stu-id="d349c-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="d349c-257">Você pode ajudar a reduzir o número de saudação de tais ocorrências marcando o evento de risco hello como falsos positivos.</span><span class="sxs-lookup"><span data-stu-id="d349c-257">You can help reduce hello number of such occurrences by marking hello risk event as False-positive.</span></span> <span data-ttu-id="d349c-258">Isso ajudará a classificação de saudação tooimprove algoritmos de eventos semelhantes no futuro de saudação do aprendizado de máquina hello.</span><span class="sxs-lookup"><span data-stu-id="d349c-258">This will help hello machine learning algorithms tooimprove hello classification of similar events in hello future.</span></span> <span data-ttu-id="d349c-259">status de saudação de eventos de falso positivo é muito**fechado** e eles não são mais contribuirá toouser risco.</span><span class="sxs-lookup"><span data-stu-id="d349c-259">hello status of false-positive events is too**Closed** and they will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="d349c-260">**Ignorar** - se você não executou a qualquer ação de correção, mas desejar Olá toobe de evento de risco removido da lista de ativos hello, você pode marcar um evento de risco ignorar e status de evento Olá será fechada.</span><span class="sxs-lookup"><span data-stu-id="d349c-260">**Ignore** - If you have not taken any remediation action, but want hello risk event toobe removed from hello active list, you can mark a risk event Ignore and hello event status will be Closed.</span></span> <span data-ttu-id="d349c-261">Eventos ignorados não contribuem toouser risco.</span><span class="sxs-lookup"><span data-stu-id="d349c-261">Ignored events do not contribute toouser risk.</span></span> <span data-ttu-id="d349c-262">Essa opção deve ser usada somente em circunstâncias incomuns.</span><span class="sxs-lookup"><span data-stu-id="d349c-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="d349c-263">**Reativar** -corre o risco de eventos que foram fechados manualmente (escolhendo **resolver**, **falso positivo**, ou **ignorar**) pode ser reativado, definindo Olá status de evento novamente muito**Active**.</span><span class="sxs-lookup"><span data-stu-id="d349c-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting hello event status back too**Active**.</span></span> <span data-ttu-id="d349c-264">Eventos de risco reativado contribuem cálculo do nível de risco do usuário toohello.</span><span class="sxs-lookup"><span data-stu-id="d349c-264">Reactivated risk events contribute toohello user risk level calculation.</span></span> <span data-ttu-id="d349c-265">Eventos de risco fechados por meio de correção (como redefinir uma senha de segurança) não podem ser reativados.</span><span class="sxs-lookup"><span data-stu-id="d349c-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="d349c-266">**caixa de diálogo de configuração relacionados de saudação tooopen**:</span><span class="sxs-lookup"><span data-stu-id="d349c-266">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="d349c-267">Em Olá **Azure AD Identity Protection** folha, em **investigar**, clique em **eventos de risco**.</span><span class="sxs-lookup"><span data-stu-id="d349c-267">On hello **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="d349c-268">![Redefinição de senha manual](./media/active-directory-identityprotection/1002.png "Redefinição de senha manual")</span><span class="sxs-lookup"><span data-stu-id="d349c-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="d349c-269">Em Olá **eventos de risco** lista, clique em um risco.</span><span class="sxs-lookup"><span data-stu-id="d349c-269">In hello **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="d349c-270">![Redefinição de senha manual](./media/active-directory-identityprotection/1003.png "Redefinição de senha manual")</span><span class="sxs-lookup"><span data-stu-id="d349c-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="d349c-271">Na folha de risco hello, clique em um usuário.</span><span class="sxs-lookup"><span data-stu-id="d349c-271">On hello risk blade, right-click a user.</span></span>

    <span data-ttu-id="d349c-272">![Redefinição de senha manual](./media/active-directory-identityprotection/1004.png "Redefinição de senha manual")</span><span class="sxs-lookup"><span data-stu-id="d349c-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="d349c-273">Fechar manualmente todos os eventos de risco para um usuário</span><span class="sxs-lookup"><span data-stu-id="d349c-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="d349c-274">Em vez de fechar manualmente os eventos de risco de um usuário individualmente, proteção de identidade do Azure Active Directory também fornece um método tooclose todos os eventos para um usuário com um clique.</span><span class="sxs-lookup"><span data-stu-id="d349c-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method tooclose all events for a user with one click.</span></span>

<span data-ttu-id="d349c-275">![Ações](./media/active-directory-identityprotection/2222.png "Ações")</span><span class="sxs-lookup"><span data-stu-id="d349c-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="d349c-276">Quando você clica em **descartar todos os eventos**, todos os eventos estão fechados e usuário Olá afetado não está mais em risco.</span><span class="sxs-lookup"><span data-stu-id="d349c-276">When you click **Dismiss all events**, all events are closed and hello affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="d349c-277">Corrigir eventos de risco do usuário</span><span class="sxs-lookup"><span data-stu-id="d349c-277">Remediating user risk events</span></span>

<span data-ttu-id="d349c-278">Uma solução é toosecure uma ação que uma identidade ou um dispositivo que foi anteriormente suspeita ou toobe comprometido.</span><span class="sxs-lookup"><span data-stu-id="d349c-278">A remediation is an action toosecure an identity or a device that was previously suspected or known toobe compromised.</span></span> <span data-ttu-id="d349c-279">Uma ação de correção restaura Olá identidade ou dispositivo tooa seguro estado e resolve anterior eventos de risco associados à identidade hello ou dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d349c-279">A remediation action restores hello identity or device tooa safe state, and resolves previous risk events associated with hello identity or device.</span></span>

<span data-ttu-id="d349c-280">eventos de risco do usuário tooremediate, você pode:</span><span class="sxs-lookup"><span data-stu-id="d349c-280">tooremediate user risk events, you can:</span></span>

* <span data-ttu-id="d349c-281">Executar eventos de risco de usuário uma senha segura redefinição tooremediate manualmente</span><span class="sxs-lookup"><span data-stu-id="d349c-281">Perform a secure password reset tooremediate user risk events manually</span></span>
* <span data-ttu-id="d349c-282">Configurar um toomitigate de política de segurança do usuário risco ou corrigir eventos de risco do usuário automaticamente</span><span class="sxs-lookup"><span data-stu-id="d349c-282">Configure a user risk security policy toomitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="d349c-283">Recriar a imagem de dispositivo de saudação infectado</span><span class="sxs-lookup"><span data-stu-id="d349c-283">Re-image hello infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="d349c-284">Redefinição de senha de segurança manual</span><span class="sxs-lookup"><span data-stu-id="d349c-284">Manual secure password reset</span></span>
<span data-ttu-id="d349c-285">Uma redefinição de senha segura é uma solução eficaz para muitos eventos de risco e quando executada, automaticamente fecha esses eventos de risco e recalcula o nível de risco do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="d349c-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates hello user risk level.</span></span> <span data-ttu-id="d349c-286">Você pode usar o hello Identity Protection painel tooinitiate uma redefinição de senha para um usuário arriscado.</span><span class="sxs-lookup"><span data-stu-id="d349c-286">You can use hello Identity Protection dashboard tooinitiate a password reset for a risky user.</span></span>

<span data-ttu-id="d349c-287">diálogo relacionadas Olá fornece tooreset de dois métodos diferentes de uma senha:</span><span class="sxs-lookup"><span data-stu-id="d349c-287">hello related dialog provides two different methods tooreset a password:</span></span>

<span data-ttu-id="d349c-288">**Redefinir senha** - selecione **exigem Olá usuário tooreset sua senha** tooallow Olá recuperação do usuário tooself se Olá usuário tiver registrado para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="d349c-288">**Reset password** - Select **Require hello user tooreset their password** tooallow hello user tooself-recover if hello user has registered for multi-factor authentication.</span></span> <span data-ttu-id="d349c-289">Durante a saudação do próximo logon do usuário, o usuário de saudação será toosolve necessária uma autenticação multifator com êxito o desafio e a senha de Olá toochange em seguida, forçado.</span><span class="sxs-lookup"><span data-stu-id="d349c-289">During hello user's next sign-in, hello user will be required toosolve a multi-factor authentication challenge successfully and then, forced toochange hello password.</span></span> <span data-ttu-id="d349c-290">Essa opção não estará disponível se a conta de usuário de saudação não estiver registrado a autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="d349c-290">This option isn't available if hello user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="d349c-291">**Senha temporária** - selecione **gerar uma senha temporária** tooimmediately invalidar senha existente hello e criar uma nova senha temporária para o usuário hello.</span><span class="sxs-lookup"><span data-stu-id="d349c-291">**Temporary password** - Select **Generate a temporary password** tooimmediately invalidate hello existing password, and create a new temporary password for hello user.</span></span> <span data-ttu-id="d349c-292">Envie Olá nova senha temporária tooan endereço de email alternativo para o usuário hello ou o gerente do usuário toohello.</span><span class="sxs-lookup"><span data-stu-id="d349c-292">Send hello new temporary password tooan alternate email address for hello user or toohello user's manager.</span></span> <span data-ttu-id="d349c-293">Como senha Olá é temporária, usuário Olá será senha de saudação toochange solicitada ao entrar.</span><span class="sxs-lookup"><span data-stu-id="d349c-293">Because hello password is temporary, hello user will be prompted toochange hello password upon sign-in.</span></span>

<span data-ttu-id="d349c-294">![Política](./media/active-directory-identityprotection/1005.png "Política")</span><span class="sxs-lookup"><span data-stu-id="d349c-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="d349c-295">**caixa de diálogo de configuração relacionados de saudação tooopen**:</span><span class="sxs-lookup"><span data-stu-id="d349c-295">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="d349c-296">Em Olá **Azure AD Identity Protection** folha, clique em **usuários sinalizados riscos**.</span><span class="sxs-lookup"><span data-stu-id="d349c-296">On hello **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="d349c-297">![Redefinição de senha manual](./media/active-directory-identityprotection/1006.png "Redefinição de senha manual")</span><span class="sxs-lookup"><span data-stu-id="d349c-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="d349c-298">Na lista de saudação de usuários, selecione um usuário com eventos de pelo menos um risco.</span><span class="sxs-lookup"><span data-stu-id="d349c-298">From hello list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="d349c-299">![Redefinição de senha manual](./media/active-directory-identityprotection/1007.png "Redefinição de senha manual")</span><span class="sxs-lookup"><span data-stu-id="d349c-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="d349c-300">Na folha de usuário hello, clique em **Redefinir senha**.</span><span class="sxs-lookup"><span data-stu-id="d349c-300">On hello user blade, click **Reset password**.</span></span>

    <span data-ttu-id="d349c-301">![Redefinição de senha manual](./media/active-directory-identityprotection/1008.png "Redefinição de senha manual")</span><span class="sxs-lookup"><span data-stu-id="d349c-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="d349c-302">Política de segurança de risco do usuário</span><span class="sxs-lookup"><span data-stu-id="d349c-302">User risk security policy</span></span>
<span data-ttu-id="d349c-303">Uma política de segurança do usuário risco é uma política de acesso condicional que avalia um usuário específico do nível tooa Olá risco e aplica as ações de correção e atenuação com base em regras e condições predefinidas.</span><span class="sxs-lookup"><span data-stu-id="d349c-303">A user risk security policy is a conditional access policy that evaluates hello risk level tooa specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="d349c-304">![Política do usuário ridk](./media/active-directory-identityprotection/1009.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="d349c-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="d349c-305">O Azure AD Identity Protection ajuda você a gerenciar a atenuação hello e correção de usuários sinalizados riscos, permitindo que você:</span><span class="sxs-lookup"><span data-stu-id="d349c-305">Azure AD Identity Protection helps you manage hello mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="d349c-306">Definir Olá usuários e grupos Olá política aplica-se a:</span><span class="sxs-lookup"><span data-stu-id="d349c-306">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="d349c-307">![Política do usuário ridk](./media/active-directory-identityprotection/1010.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="d349c-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="d349c-308">Defina Olá usuário risco nível limite (baixa, média ou alta) que dispara a política de saudação:</span><span class="sxs-lookup"><span data-stu-id="d349c-308">Set hello user risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="d349c-309">![Política do usuário ridk](./media/active-directory-identityprotection/1011.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="d349c-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="d349c-310">Conjunto Olá controles toobe imposta quando a política de saudação dispara:</span><span class="sxs-lookup"><span data-stu-id="d349c-310">Set hello controls toobe enforced when hello policy triggers:</span></span>

    <span data-ttu-id="d349c-311">![Política do usuário ridk](./media/active-directory-identityprotection/1012.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="d349c-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="d349c-312">Alternar estado Olá da política:</span><span class="sxs-lookup"><span data-stu-id="d349c-312">Switch hello state of your policy:</span></span>

    <span data-ttu-id="d349c-313">![Política do usuário ridk](./media/active-directory-identityprotection/403.png "Registro de MFA")</span><span class="sxs-lookup"><span data-stu-id="d349c-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="d349c-314">Revisar e avaliar o impacto de saudação de uma alteração antes de ativá-lo:</span><span class="sxs-lookup"><span data-stu-id="d349c-314">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="d349c-315">![Política do usuário ridk](./media/active-directory-identityprotection/1013.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="d349c-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="d349c-316">Escolhendo um **alta** limite reduz o número de saudação de vezes que uma política é disparada e minimiza Olá impacto toousers.</span><span class="sxs-lookup"><span data-stu-id="d349c-316">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>
<span data-ttu-id="d349c-317">No entanto, ele exclui **baixo** e **médio** usuários sinalizados riscos da política de saudação, que pode não proteger identidades ou dispositivos que foram anteriormente suspeita ou toobe comprometida.</span><span class="sxs-lookup"><span data-stu-id="d349c-317">However, it excludes **Low** and **Medium** users flagged for risk from hello policy, which may not secure identities or devices that were previously suspected or known toobe compromised.</span></span>

<span data-ttu-id="d349c-318">Quando a configuração Olá política,</span><span class="sxs-lookup"><span data-stu-id="d349c-318">When setting hello policy,</span></span>

* <span data-ttu-id="d349c-319">Exclua os usuários que são provavelmente toogenerate muitos falsos positivos (desenvolvedores, analistas de segurança)</span><span class="sxs-lookup"><span data-stu-id="d349c-319">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="d349c-320">Exclua os usuários em locais onde habilitando Olá política não é prático (por exemplo, nenhum toohelpdesk de acesso)</span><span class="sxs-lookup"><span data-stu-id="d349c-320">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="d349c-321">use um limite **Alto** durante a distribuição inicial de política ou se você precisar minimizar os desafios encontrados pelos usuários finais.</span><span class="sxs-lookup"><span data-stu-id="d349c-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="d349c-322">use um limite **Baixo** se sua organização exigir uma segurança maior.</span><span class="sxs-lookup"><span data-stu-id="d349c-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="d349c-323">Selecionar um limite **Baixo** apresenta desafios de entrada do usuário adicionais, porém representa uma segurança maior.</span><span class="sxs-lookup"><span data-stu-id="d349c-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="d349c-324">Olá recomendado padrão para a maioria das organizações é tooconfigure uma regra para um **médio** limite toostrike um equilíbrio entre segurança e facilidade de uso.</span><span class="sxs-lookup"><span data-stu-id="d349c-324">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="d349c-325">Para obter uma visão geral de saudação relacionadas a experiência do usuário, consulte:</span><span class="sxs-lookup"><span data-stu-id="d349c-325">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="d349c-326">[Fluxo de recuperação de conta comprometida](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="d349c-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="d349c-327">[Fluxo de conta comprometida bloqueada](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="d349c-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="d349c-328">**caixa de diálogo de configuração relacionados de saudação tooopen**:</span><span class="sxs-lookup"><span data-stu-id="d349c-328">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="d349c-329">Em Olá **Azure AD Identity Protection** folha em Olá **configurar** seção, clique em **política de risco do usuário**.</span><span class="sxs-lookup"><span data-stu-id="d349c-329">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="d349c-330">![Política do usuário ridk](./media/active-directory-identityprotection/1009.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="d349c-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="d349c-331">Mitigar eventos de risco do usuário</span><span class="sxs-lookup"><span data-stu-id="d349c-331">Mitigating user risk events</span></span>
<span data-ttu-id="d349c-332">Os administradores podem definir um usuário risco política tooblock os usuários de segurança após entrar dependendo do nível de risco de saudação.</span><span class="sxs-lookup"><span data-stu-id="d349c-332">Administrators can set a user risk security policy tooblock users upon sign-in depending on hello risk level.</span></span>

<span data-ttu-id="d349c-333">Bloquear a entrada:</span><span class="sxs-lookup"><span data-stu-id="d349c-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="d349c-334">Evita a geração de saudação de novos eventos de risco de usuário para usuário Olá afetado</span><span class="sxs-lookup"><span data-stu-id="d349c-334">Prevents hello generation of new user risk events for hello affected user</span></span>
* <span data-ttu-id="d349c-335">Permite que os administradores toomanually corrigir eventos de risco Olá que afetam a identidade do usuário hello e restaure-o estado seguro tooa</span><span class="sxs-lookup"><span data-stu-id="d349c-335">Enables administrators toomanually remediate hello risk events affecting hello user's identity and restore it tooa secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="d349c-336">Política de registro de autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="d349c-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="d349c-337">Autenticação multifator do Azure é um método de verificação que você está que requer uso de saudação de mais do que apenas um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="d349c-337">Azure multi-factor authentication is a method of verifying who you are that requires hello use of more than just a username and password.</span></span> <span data-ttu-id="d349c-338">Ele fornece uma segunda camada de segurança toouser entradas e transações.</span><span class="sxs-lookup"><span data-stu-id="d349c-338">It provides a second layer of security toouser sign-ins and transactions.</span></span>  
<span data-ttu-id="d349c-339">Recomendamos exigir a autenticação multifator do Azure para entradas de usuário porque:</span><span class="sxs-lookup"><span data-stu-id="d349c-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="d349c-340">fornece autenticação forte com uma variedade de opções de verificação fácil</span><span class="sxs-lookup"><span data-stu-id="d349c-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="d349c-341">Desempenha um papel fundamental na preparação de sua organização tooprotect e recuperar o comprometimento de conta</span><span class="sxs-lookup"><span data-stu-id="d349c-341">Plays a key role in preparing your organization tooprotect and recover from account compromises</span></span>

<span data-ttu-id="d349c-342">![Política do usuário ridk](./media/active-directory-identityprotection/1019.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="d349c-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="d349c-343">Para obter mais detalhes, veja [O que é a Autenticação Multifator do Azure?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d349c-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="d349c-344">O Azure AD Identity Protection ajuda você a gerenciar Olá roll-out de um registro de autenticação multifator, configurando uma política que permite que você:</span><span class="sxs-lookup"><span data-stu-id="d349c-344">Azure AD Identity Protection helps you manage hello roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="d349c-345">Definir Olá usuários e grupos Olá política aplica-se a:</span><span class="sxs-lookup"><span data-stu-id="d349c-345">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="d349c-346">![Política de MFA](./media/active-directory-identityprotection/1020.png "Política de MFA")</span><span class="sxs-lookup"><span data-stu-id="d349c-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="d349c-347">Conjunto Olá controles toobe imposta quando a política de saudação dispara::</span><span class="sxs-lookup"><span data-stu-id="d349c-347">Set hello controls toobe enforced when hello policy triggers::</span></span>  

    <span data-ttu-id="d349c-348">![Política de MFA](./media/active-directory-identityprotection/1021.png "Política de MFA")</span><span class="sxs-lookup"><span data-stu-id="d349c-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="d349c-349">Alternar estado Olá da política:</span><span class="sxs-lookup"><span data-stu-id="d349c-349">Switch hello state of your policy:</span></span>

    <span data-ttu-id="d349c-350">![Política de MFA](./media/active-directory-identityprotection/403.png "Política de MFA")</span><span class="sxs-lookup"><span data-stu-id="d349c-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="d349c-351">Exibir o status de registro atual hello:</span><span class="sxs-lookup"><span data-stu-id="d349c-351">View hello current registration status:</span></span>

    <span data-ttu-id="d349c-352">![Política de MFA](./media/active-directory-identityprotection/1022.png "Política de MFA")</span><span class="sxs-lookup"><span data-stu-id="d349c-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="d349c-353">Para obter uma visão geral de saudação relacionadas a experiência do usuário, consulte:</span><span class="sxs-lookup"><span data-stu-id="d349c-353">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="d349c-354">[Fluxo do registro de autenticação multifator](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="d349c-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="d349c-355">[Experiências de entrada com o Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="d349c-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="d349c-356">**caixa de diálogo de configuração relacionados de saudação tooopen**:</span><span class="sxs-lookup"><span data-stu-id="d349c-356">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="d349c-357">Em Olá **Azure AD Identity Protection** folha em Olá **configurar** seção, clique em **registro de autenticação multifator**.</span><span class="sxs-lookup"><span data-stu-id="d349c-357">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="d349c-358">![Política de MFA](./media/active-directory-identityprotection/1019.png "Política de MFA")</span><span class="sxs-lookup"><span data-stu-id="d349c-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="d349c-359">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d349c-359">Next steps</span></span>
* [<span data-ttu-id="d349c-360">Canal 9: Azure AD e Identity Show: visualização do Identity Protection</span><span class="sxs-lookup"><span data-stu-id="d349c-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="d349c-361">Habilitando o Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="d349c-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="d349c-362">Vulnerabilidades detectadas pelo Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="d349c-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="d349c-363">Eventos de risco do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d349c-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="d349c-364">Notificações do Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="d349c-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="d349c-365">Guia estratégico do Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="d349c-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="d349c-366">Glossário do Azure Active Directory Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="d349c-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="d349c-367">Experiências de entrada com o Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="d349c-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="d349c-368">Proteção do Azure Active Directory identidade - como toounblock usuários</span><span class="sxs-lookup"><span data-stu-id="d349c-368">Azure Active Directory Identity Protection - How toounblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="d349c-369">Introdução ao Azure Active Directory Identity Protection e ao Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="d349c-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
