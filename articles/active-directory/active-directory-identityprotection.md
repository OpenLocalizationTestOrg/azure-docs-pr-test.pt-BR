---
title: Azure Active Directory Identity Protection | Microsoft Docs
description: Saiba como o Azure AD Identity Protection permite limitar a capacidade de um invasor de explorar uma identidade ou um dispositivo comprometidos ou um dispositivo que sofreu comprometimento conhecido ou suspeito anteriormente.
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
ms.openlocfilehash: 0c7a8d68c0df729441e3f7faa5cd06066db1261d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="3b5f6-104">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3b5f6-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="3b5f6-105">O Azure Active Directory Identity Protection é um recurso da edição Premium P2 do Azure AD que permite a você:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-105">Azure Active Directory Identity Protection is a feature of the Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="3b5f6-106">Detectar possíveis vulnerabilidades que afetam as identidades da organização</span><span class="sxs-lookup"><span data-stu-id="3b5f6-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="3b5f6-107">Configurar respostas automatizadas para ações suspeitas detectadas que se relacionem com as identidades da sua organização</span><span class="sxs-lookup"><span data-stu-id="3b5f6-107">Configure automated responses to detected suspicious actions that are related to your organization’s identities</span></span>  

- <span data-ttu-id="3b5f6-108">Investigar incidentes suspeitos e tomar as devidas providências para resolvê-los</span><span class="sxs-lookup"><span data-stu-id="3b5f6-108">Investigate suspicious incidents and take appropriate action to resolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="3b5f6-109">Introdução</span><span class="sxs-lookup"><span data-stu-id="3b5f6-109">Getting started</span></span>

<span data-ttu-id="3b5f6-110">A Microsoft protege identidades baseadas em nuvem há mais de uma década.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="3b5f6-111">Com o Azure Active Directory Identity Protection, você pode usar os mesmos sistemas de proteção em seu ambiente que a Microsoft usa para proteger as identidades.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-111">With Azure Active Directory Identity Protection, in your environment, you can use the same protection systems Microsoft uses to secure identities.</span></span>

<span data-ttu-id="3b5f6-112">A grande maioria das violações de segurança ocorre quando os invasores conseguem acessar a um ambiente roubando a identidade de um usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-112">The vast majority of security breaches take place when attackers gain access to an environment by stealing a user’s identity.</span></span> <span data-ttu-id="3b5f6-113">Nos últimos anos, os invasores têm se tornado cada vez mais eficazes em aproveitar as violações de terceiros e usar ataques de phishing sofisticados.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-113">Over the years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="3b5f6-114">Assim que um invasor obtém acesso até mesmo a uma conta de usuário com privilégios baixos, é relativamente fácil para ele conseguir acessar recursos importantes da empresa por meio de movimentação lateral.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-114">As soon as an attacker gains access to even low privileged user accounts, it is relatively easy for them to gain access to important company resources through lateral movement.</span></span>

<span data-ttu-id="3b5f6-115">Como consequência, você precisa:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="3b5f6-116">Proteger todas as identidades, independentemente do nível de privilégio</span><span class="sxs-lookup"><span data-stu-id="3b5f6-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="3b5f6-117">Agir proativamente para evitar o uso de identidades comprometidas</span><span class="sxs-lookup"><span data-stu-id="3b5f6-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="3b5f6-118">Descobrir identidades comprometidas não é uma tarefa fácil.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="3b5f6-119">O Azure Active Directory usa algoritmos de aprendizado de máquina e heurística adaptáveis para detectar anomalias e incidentes suspeitos que indicam identidades potencialmente comprometidas.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="3b5f6-120">Usando esses dados, o Identity Protection gera relatórios e alertas que permitem avaliar os problemas detectados e tomar as devidas ações de mitigação ou correção.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-120">Using this data, Identity Protection generates reports and alerts that enable you to evaluate the detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="3b5f6-121">O Azure Active Directory Identity Protection é mais do que apenas uma ferramenta de monitoramento e criação de relatórios.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="3b5f6-122">Para proteger as identidades da sua organização, você pode configurar políticas de risco que respondem automaticamente a problemas detectados quando um nível de risco especificado foi alcançado.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-122">To protect your organization's identities, you can configure risk-based policies that automatically respond to detected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="3b5f6-123">Essas políticas, entre outros controles de acesso condicional fornecidos pelo Azure Active Directory e pelo EMS, podem bloquear ou iniciar automaticamente ações de correção adaptáveis que incluem redefinições de senha e a imposição de autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-123">These policies, in addition to other conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="3b5f6-124">Recursos do Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3b5f6-124">Identity Protection capabilities</span></span>

<span data-ttu-id="3b5f6-125">**Detecção de vulnerabilidades e contas de risco:**</span><span class="sxs-lookup"><span data-stu-id="3b5f6-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="3b5f6-126">Fornecer recomendações personalizadas para melhorar a postura de segurança geral ao realçar as vulnerabilidades</span><span class="sxs-lookup"><span data-stu-id="3b5f6-126">Providing custom recommendations to improve overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="3b5f6-127">Calcular os níveis de risco de entrada</span><span class="sxs-lookup"><span data-stu-id="3b5f6-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="3b5f6-128">Calcular os níveis de risco do usuário</span><span class="sxs-lookup"><span data-stu-id="3b5f6-128">Calculating user risk levels</span></span>


<span data-ttu-id="3b5f6-129">**Investigação dos eventos de risco:**</span><span class="sxs-lookup"><span data-stu-id="3b5f6-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="3b5f6-130">Enviar notificações para eventos de risco</span><span class="sxs-lookup"><span data-stu-id="3b5f6-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="3b5f6-131">Investigar os eventos de risco usando informações relevantes e contextuais</span><span class="sxs-lookup"><span data-stu-id="3b5f6-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="3b5f6-132">Fornecer fluxos de trabalho básicos para acompanhar as investigações</span><span class="sxs-lookup"><span data-stu-id="3b5f6-132">Providing basic workflows to track investigations</span></span>
* <span data-ttu-id="3b5f6-133">Fornecer acesso fácil às ações de correção, tais como redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="3b5f6-133">Providing easy access to remediation actions such as password reset</span></span>

<span data-ttu-id="3b5f6-134">**Políticas de acesso condicional baseadas em risco:**</span><span class="sxs-lookup"><span data-stu-id="3b5f6-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="3b5f6-135">Política para reduzir entradas arriscadas ao bloquear entradas ou exigir desafios de autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-135">Policy to mitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="3b5f6-136">Política para bloquear ou proteger contas de usuário arriscadas</span><span class="sxs-lookup"><span data-stu-id="3b5f6-136">Policy to block or secure risky user accounts</span></span>
* <span data-ttu-id="3b5f6-137">Política para exigir o registro para autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="3b5f6-137">Policy to require users to register for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="3b5f6-138">Funções da proteção de identidade</span><span class="sxs-lookup"><span data-stu-id="3b5f6-138">Identity Protection roles</span></span>

<span data-ttu-id="3b5f6-139">Para equilibrar as atividades de gerenciamento em torno de sua implementação da proteção de identidade, você pode atribuir várias funções.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-139">To load balance the management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="3b5f6-140">O Azure AD Identity Protection dá suporte a três funções do diretório:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="3b5f6-141">Função</span><span class="sxs-lookup"><span data-stu-id="3b5f6-141">Role</span></span>                         | <span data-ttu-id="3b5f6-142">O que ele pode fazer</span><span class="sxs-lookup"><span data-stu-id="3b5f6-142">Can do</span></span>                          | <span data-ttu-id="3b5f6-143">O que não pode fazer</span><span class="sxs-lookup"><span data-stu-id="3b5f6-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="3b5f6-144">Administrador global</span><span class="sxs-lookup"><span data-stu-id="3b5f6-144">Global administrator</span></span>         | <span data-ttu-id="3b5f6-145">Acesso completo à Proteção de Identidade, Proteção de Identidade integrada</span><span class="sxs-lookup"><span data-stu-id="3b5f6-145">Full access to Identity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="3b5f6-146">Administrador de segurança</span><span class="sxs-lookup"><span data-stu-id="3b5f6-146">Security administrator</span></span>       | <span data-ttu-id="3b5f6-147">Acesso total à proteção de identidade</span><span class="sxs-lookup"><span data-stu-id="3b5f6-147">Full access to Identity Protection</span></span> | <span data-ttu-id="3b5f6-148">Proteção de Identidade integrada, redefinir senhas para um usuário</span><span class="sxs-lookup"><span data-stu-id="3b5f6-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="3b5f6-149">Leitor de segurança</span><span class="sxs-lookup"><span data-stu-id="3b5f6-149">Security reader</span></span>              | <span data-ttu-id="3b5f6-150">Acesso somente de leitura para a Proteção de Identidade</span><span class="sxs-lookup"><span data-stu-id="3b5f6-150">Ready-only access to Identity Protection</span></span> | <span data-ttu-id="3b5f6-151">Integrar Proteção de Identidade, corrigir usuários, configurar políticas, redefinir senhas</span><span class="sxs-lookup"><span data-stu-id="3b5f6-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="3b5f6-152">Para saber mais detalhes, consulte [Atribuindo funções de administrador no Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3b5f6-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="3b5f6-153">Detecção</span><span class="sxs-lookup"><span data-stu-id="3b5f6-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="3b5f6-154">Vulnerabilidades</span><span class="sxs-lookup"><span data-stu-id="3b5f6-154">Vulnerabilities</span></span>

<span data-ttu-id="3b5f6-155">O Azure Active Directory Identity Protection analisa sua configuração e detecta vulnerabilidades que podem ter impacto nas identidades do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="3b5f6-156">Para saber mais, confira [Vulnerabilidades detectadas pelo Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="3b5f6-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="3b5f6-157">Eventos de risco</span><span class="sxs-lookup"><span data-stu-id="3b5f6-157">Risk events</span></span>

<span data-ttu-id="3b5f6-158">O Azure Active Directory usa algoritmos de aprendizado de máquina e heurística adaptáveis para detectar ações suspeitas relacionadas a identidades do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user's identities.</span></span> <span data-ttu-id="3b5f6-159">O sistema cria um registro para cada ação suspeita detectada.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-159">The system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="3b5f6-160">Esses registros também são conhecidos como eventos de risco.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="3b5f6-161">Para obter mais detalhes, veja [Eventos de risco do Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="3b5f6-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="3b5f6-162">Investigação</span><span class="sxs-lookup"><span data-stu-id="3b5f6-162">Investigation</span></span>
<span data-ttu-id="3b5f6-163">Sua jornada pelo Identity Protection normalmente inicia no Painel do Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-163">Your journey through Identity Protection typically starts with the Identity Protection dashboard.</span></span>

<span data-ttu-id="3b5f6-164">![Correção](./media/active-directory-identityprotection/1000.png "Correção")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="3b5f6-165">O painel concede acesso a:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-165">The dashboard gives you access to:</span></span>

* <span data-ttu-id="3b5f6-166">Relatórios, como **Usuários sinalizados por riscos**, **Eventos de risco** e **Vulnerabilidades**</span><span class="sxs-lookup"><span data-stu-id="3b5f6-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="3b5f6-167">Configurações como a definição das suas **Políticas de Segurança**, **Notificações** e **registro de autenticação multifator**</span><span class="sxs-lookup"><span data-stu-id="3b5f6-167">Settings such as the configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="3b5f6-168">Este é normalmente seu ponto de partida para investigação, que é o processo de revisão de atividades, logs e outras informações relevantes relacionadas a um evento de risco para decidir se as etapas de correção e mitigação são necessárias, como a identidade foi comprometida e entender como ela foi usada.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-168">It is typically your starting point for investigation, which is the process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary,  and how the identity was compromised, and understand how the compromised identity was used.</span></span>

<span data-ttu-id="3b5f6-169">Você pode vincular suas atividades de investigação para as [notificações](active-directory-identityprotection-notifications.md) que o Azure Active Directory Protection envia por email.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-169">You can tie your investigation activities to the [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="3b5f6-170">As seções a seguir fornecerão mais detalhes e as etapas que estão relacionadas a uma investigação.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-170">The following sections provide you with more details and the steps that are related to an investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="3b5f6-171">Entradas de risco</span><span class="sxs-lookup"><span data-stu-id="3b5f6-171">Risky sign-ins</span></span>

<span data-ttu-id="3b5f6-172">O Azure Active Directory detecta [tipos de evento de risco](active-directory-reporting-risk-events.md#risk-event-types) em tempo real e offline.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="3b5f6-173">Cada evento de risco que tiver sido detectado para a entrada de um usuário contribui para um conceito lógico chamado entrada de risco.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-173">Each risk event that has been detected for a sign-in of a user contributes to a logical concept called risky sign-in.</span></span> <span data-ttu-id="3b5f6-174">Uma entrada de risco é um indicador de uma tentativa de logon que pode não ter sido realizada pelo proprietário legítimo de uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by the legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="3b5f6-175">Nível de risco de entrada</span><span class="sxs-lookup"><span data-stu-id="3b5f6-175">Sign-in risk level</span></span>

<span data-ttu-id="3b5f6-176">Um nível de risco de entrada é uma indicação (alta, média ou baixa) da probabilidade de uma tentativa de logon não ter sido executada pelo proprietário legítimo de uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-176">A sign-in risk level is an indication (High, Medium, or Low) of the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="3b5f6-177">Mitigação de eventos de risco de entrada</span><span class="sxs-lookup"><span data-stu-id="3b5f6-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="3b5f6-178">Uma mitigação é uma ação que visa limitar a capacidade de um invasor explorar uma identidade ou um dispositivo comprometidos sem restaurá-los para um estado seguro.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-178">A mitigation is an action to limit the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="3b5f6-179">Uma mitigação não resolve eventos de risco de entrada anteriores associados à identidade ou ao dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-179">A mitigation does not resolve previous sign-in risk events associated with the identity or device.</span></span>

<span data-ttu-id="3b5f6-180">Para atenuar as entradas de risco automaticamente, você pode configurar políticas de segurança de entradas de risco.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-180">To mitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="3b5f6-181">Ao usar essas políticas, considere o nível de risco do usuário ou da entrada para bloquear entradas arriscadas ou exigir que o usuário realize a autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-181">Using these policies, you consider the risk level of the user or the sign-in to block risky sign-ins or require the user to perform multi-factor authentication.</span></span> <span data-ttu-id="3b5f6-182">Essas ações podem impedir que um invasor explore uma identidade roubada para causar danos, fazendo você ganhar algum tempo para proteger a identidade.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-182">These actions may prevent an attacker from exploiting a stolen identity to cause damage, and may give you some time to secure the identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="3b5f6-183">Política de segurança de risco de entrada</span><span class="sxs-lookup"><span data-stu-id="3b5f6-183">Sign-in risk security policy</span></span>
<span data-ttu-id="3b5f6-184">Uma política de segurança de risco de entrada é uma política de acesso condicional que avalia o risco de uma entrada específica e aplica mitigações com base em regras e condições predefinidas.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-184">A sign-in risk policy is a conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="3b5f6-185">![Política de risco de entrada](./media/active-directory-identityprotection/1014.png "Política de risco de entrada")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="3b5f6-186">O Azure AD Identity Protection ajuda a gerenciar a mitigação de entradas arriscadas, permitindo:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-186">Azure AD Identity Protection helps you manage the mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="3b5f6-187">Defina os usuários e os grupos aos quais a política se aplica:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-187">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="3b5f6-188">![Política de risco de entrada](./media/active-directory-identityprotection/1015.png "Política de risco de entrada")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="3b5f6-189">Defina o limite de nível de risco da entrada (baixo, médio ou alto) que dispara o bloqueio de um usuário:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-189">Set the sign-in risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="3b5f6-190">![Política de risco de entrada](./media/active-directory-identityprotection/1016.png "Política de risco de entrada")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="3b5f6-191">Defina os controles a serem impostos quando a política for disparada:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-191">Set the controls to be enforced when the policy triggers:</span></span>  

    <span data-ttu-id="3b5f6-192">![Política de risco de entrada](./media/active-directory-identityprotection/1017.png "Política de risco de entrada")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="3b5f6-193">Alterne o estado de sua política:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-193">Switch the state of your policy:</span></span>

    <span data-ttu-id="3b5f6-194">![Registro de MFA](./media/active-directory-identityprotection/403.png "Registro de MFA")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="3b5f6-195">Examine e avalie o impacto de uma alteração antes de ativá-la:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-195">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="3b5f6-196">![Política de risco de entrada](./media/active-directory-identityprotection/1018.png "Política de risco de entrada")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-to-know"></a><span data-ttu-id="3b5f6-197">O que você precisa saber</span><span class="sxs-lookup"><span data-stu-id="3b5f6-197">What you need to know</span></span>
<span data-ttu-id="3b5f6-198">Você pode configurar uma política de segurança de risco de entrada para exigir autenticação multifator:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-198">You can configure a sign-in risk security policy to require multi-factor authentication:</span></span>

<span data-ttu-id="3b5f6-199">![Política de risco de entrada](./media/active-directory-identityprotection/1017.png "Política de risco de entrada")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="3b5f6-200">No entanto, por motivos de segurança, essa configuração só funciona para usuários que já foram registrados na autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="3b5f6-201">Se a condição de exigir autenticação multifator for atendida por um usuário que ainda não está registrado na autenticação multifator, ele será bloqueado.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-201">If the condition to require multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, the user is blocked.</span></span>

<span data-ttu-id="3b5f6-202">Como prática recomendada, se você quiser exigir a autenticação multifator para entradas de risco:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-202">As a best practice, if you want to require multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="3b5f6-203">Habilite a [política de registro de autenticação multifator](#multi-factor-authentication-registration-policy) para os usuários afetados.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-203">Enable the [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for the affected users.</span></span>
2. <span data-ttu-id="3b5f6-204">Exija que os usuários afetados façam logon em uma sessão sem risco para realizar um registro MFA</span><span class="sxs-lookup"><span data-stu-id="3b5f6-204">Require the affected users to login in a non-risky session to perform a MFA registration</span></span>

<span data-ttu-id="3b5f6-205">A conclusão dessas etapas faz com que a autenticação multifator seja exigida em caso de entrada de risco.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="3b5f6-206">Práticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="3b5f6-206">Best practices</span></span>
<span data-ttu-id="3b5f6-207">Escolher um limite **Alto** reduz o número de vezes que uma política é disparada e minimiza o impacto para os usuários.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-207">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>  

<span data-ttu-id="3b5f6-208">No entanto, isso exclui entradas sinalizadas com **Baixo** e **Médio** risco da política, o que pode não impedir que um invasor explore uma identidade comprometida.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from the policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="3b5f6-209">Ao definir a política,</span><span class="sxs-lookup"><span data-stu-id="3b5f6-209">When setting the policy,</span></span>

* <span data-ttu-id="3b5f6-210">exclua os usuários que não tem / não podem ter a autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="3b5f6-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="3b5f6-211">exclua os usuários em localidades em que não é viável habilitar a política (por exemplo, sem acesso à assistência técnica)</span><span class="sxs-lookup"><span data-stu-id="3b5f6-211">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="3b5f6-212">exclua os usuários que tendem a gerar muitos falsos positivos (desenvolvedores e analistas de segurança)</span><span class="sxs-lookup"><span data-stu-id="3b5f6-212">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="3b5f6-213">use um limite **Alto** durante a distribuição inicial de política ou se você precisar minimizar os desafios encontrados pelos usuários finais.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="3b5f6-214">Use um limite **Baixo** se sua organização exigir uma segurança maior.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="3b5f6-215">Selecionar um limite **Baixo** apresenta desafios de entrada do usuário adicionais, porém representa uma segurança maior.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="3b5f6-216">O padrão recomendado na maioria das organizações é configurar uma regra para um limite **Médio** para atingir um equilíbrio entre segurança e usabilidade.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-216">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="3b5f6-217">A política de risco de entrada:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-217">The sign-in risk policy is:</span></span>

* <span data-ttu-id="3b5f6-218">é aplicada a todo o tráfego do navegador e entradas que usam autenticação moderna.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-218">Applied to all browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="3b5f6-219">Não é aplicada a aplicativos que usam protocolos de segurança mais antigos desabilitando o ponto de extremidade WS-Trust no IDP federado, como o ADFS.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-219">Not applied to applications using older security protocols by disabling the WS-Trust endpoint at the federated IDP, such as ADFS.</span></span>

<span data-ttu-id="3b5f6-220">A página **Eventos de Risco** no console do Identity Protection lista todos os eventos:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-220">The **Risk Events** page in the Identity Protection console lists all events:</span></span>

* <span data-ttu-id="3b5f6-221">aos quais essa política se aplica</span><span class="sxs-lookup"><span data-stu-id="3b5f6-221">This policy was applied to</span></span>
* <span data-ttu-id="3b5f6-222">para os quais você pode examinar a atividade e determinar se a ação foi apropriada ou não</span><span class="sxs-lookup"><span data-stu-id="3b5f6-222">You can review the activity and determine whether the action was appropriate or not</span></span>

<span data-ttu-id="3b5f6-223">Para obter uma visão geral da experiência do usuário relacionada, confira:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-223">For an overview of the related user experience, see:</span></span>

* [<span data-ttu-id="3b5f6-224">Recuperação de entrada arriscada</span><span class="sxs-lookup"><span data-stu-id="3b5f6-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="3b5f6-225">Entrada arriscada bloqueada</span><span class="sxs-lookup"><span data-stu-id="3b5f6-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="3b5f6-226">Experiências de entrada com o Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3b5f6-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="3b5f6-227">**Para abrir o diálogo de configurações relacionadas**:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-227">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="3b5f6-228">Na folha **Azure AD Identity Protection**, na seção **Configurar**, clique em **Política de entrada de risco**.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-228">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="3b5f6-229">![Política do usuário ridk](./media/active-directory-identityprotection/1014.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="3b5f6-230">Usuários sinalizados por risco</span><span class="sxs-lookup"><span data-stu-id="3b5f6-230">Users flagged for risk</span></span>

<span data-ttu-id="3b5f6-231">Todos os [eventos de risco](active-directory-identity-protection-risk-events.md) ativos que foram detectados pelo Azure Active Directory para um usuário contribuem para um conceito lógico chamado risco de usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute to a logical concept called user risk.</span></span> <span data-ttu-id="3b5f6-232">Um usuários sinalizado como de risco é um indicador de que uma conta de usuário pode ter sido comprometida.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Usuários sinalizados por risco](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="3b5f6-234">Nível de risco do usuário</span><span class="sxs-lookup"><span data-stu-id="3b5f6-234">User risk level</span></span>

<span data-ttu-id="3b5f6-235">Um nível de risco do usuário é uma indicação (Alta, Média ou Baixa) da probabilidade de que a identidade do usuário foi comprometida.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-235">A user risk level is an indication (High, Medium, or Low) of the likelihood that the user’s identity has been compromised.</span></span> <span data-ttu-id="3b5f6-236">Ele é calculado com base nos eventos de risco do usuário associados a uma identidade do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-236">It is calculated based on the user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="3b5f6-237">O status de um evento de risco é **Ativo** ou **Fechado**.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-237">The status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="3b5f6-238">Somente eventos de risco **Ativos** contribuem para o cálculo de nível de risco do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-238">Only risk events that are **Active** contribute to the user risk level calculation.</span></span>

<span data-ttu-id="3b5f6-239">O nível de risco do usuário é calculado usando as seguintes entradas:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-239">The user risk level is calculated using the following inputs:</span></span>

* <span data-ttu-id="3b5f6-240">Eventos de risco ativos que afetam o usuário</span><span class="sxs-lookup"><span data-stu-id="3b5f6-240">Active risk events impacting the user</span></span>
* <span data-ttu-id="3b5f6-241">Nível de risco desses eventos</span><span class="sxs-lookup"><span data-stu-id="3b5f6-241">Risk level of these events</span></span>
* <span data-ttu-id="3b5f6-242">Se foram tomadas ações de correção</span><span class="sxs-lookup"><span data-stu-id="3b5f6-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="3b5f6-243">![Riscos de usuário](./media/active-directory-identityprotection/1031.png "Riscos de usuário")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="3b5f6-244">Você pode usar os níveis de risco do usuário para criar políticas de acesso condicional que bloqueiam a entrada de usuários arriscados ou os obrigue a alterar sua senha com segurança.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-244">You can use the user risk levels to create conditional access policies that block risky users from signing in, or force them to securely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="3b5f6-245">Fechar eventos de risco manualmente</span><span class="sxs-lookup"><span data-stu-id="3b5f6-245">Closing risk events manually</span></span>

<span data-ttu-id="3b5f6-246">Na maioria dos casos, você tomará ações de correção, como uma redefinição de senha de segurança, para fechar automaticamente os eventos de risco.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-246">In most cases, you will take remediation actions such as a secure password reset to automatically close risk events.</span></span> <span data-ttu-id="3b5f6-247">No entanto, isso nem sempre é possível.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="3b5f6-248">É o caso, por exemplo, quando:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-248">This is, for example, the case, when:</span></span>

* <span data-ttu-id="3b5f6-249">um usuário com eventos de risco ativo foi excluído</span><span class="sxs-lookup"><span data-stu-id="3b5f6-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="3b5f6-250">uma investigação revela que um evento de risco relatado foi executado pelo usuário legítimo</span><span class="sxs-lookup"><span data-stu-id="3b5f6-250">An investigation reveals that a reported risk event has been perform by the legitimate user</span></span>

<span data-ttu-id="3b5f6-251">Já que eventos de risco **Ativos** contribuem para o cálculo de risco do usuário, talvez seja necessário reduzir manualmente um nível de risco fechando eventos de risco manualmente.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-251">Because risk events that are **Active** contribute to the user risk calculation, you may have to manually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="3b5f6-252">Durante a investigação, você pode optar por executar uma das seguintes ações para alterar o status de um evento de risco:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-252">During the course of investigation, you can choose to take any of these actions to change the status of a risk event:</span></span>

<span data-ttu-id="3b5f6-253">![Ações](./media/active-directory-identityprotection/34.png "Ações")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="3b5f6-254">**Resolver** - Se, após investigar um evento de risco, você tomou uma ação de correção apropriada fora do Identity Protection e acredita que o evento de risco deve ser considerado fechado, marque o evento como Resolvido.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that the risk event should be considered closed, mark the event as Resolved.</span></span> <span data-ttu-id="3b5f6-255">Eventos resolvidos definirão o status do evento de risco como Fechado e ele não contribuirá com o risco do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-255">Resolved events will set the risk event’s status to Closed and the risk event will no longer contribute to user risk.</span></span>
* <span data-ttu-id="3b5f6-256">**Marcar como falso positivo** - Em alguns casos, você pode investigar um evento de risco e descobrir que ele foi sinalizado incorretamente como uma situação arriscada.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="3b5f6-257">Você pode ajudar a reduzir o número de tais ocorrências marcando o evento de risco como falso positivo.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-257">You can help reduce the number of such occurrences by marking the risk event as False-positive.</span></span> <span data-ttu-id="3b5f6-258">Isso ajudará os algoritmos de aprendizado de máquina a melhorarem a classificação de eventos semelhantes no futuro.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-258">This will help the machine learning algorithms to improve the classification of similar events in the future.</span></span> <span data-ttu-id="3b5f6-259">O status de eventos falso positivos é **Fechado** e não contribui mais com o risco do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-259">The status of false-positive events is to **Closed** and they will no longer contribute to user risk.</span></span>
* <span data-ttu-id="3b5f6-260">**Ignorar** - Se você não executou nenhuma ação de correção, mas deseja remover o evento de risco da lista ativa, marque um evento de risco como Ignorar e o status do evento será Fechado.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-260">**Ignore** - If you have not taken any remediation action, but want the risk event to be removed from the active list, you can mark a risk event Ignore and the event status will be Closed.</span></span> <span data-ttu-id="3b5f6-261">Eventos ignorados não contribuem com o risco do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-261">Ignored events do not contribute to user risk.</span></span> <span data-ttu-id="3b5f6-262">Essa opção deve ser usada somente em circunstâncias incomuns.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="3b5f6-263">**Reativa**r - Eventos de risco fechados manualmente (escolhendo **Resolver**, **Falso positivo** ou **Ignorar**) podem ser reativados, definindo o status do evento novamente como **Ativo**.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting the event status back to **Active**.</span></span> <span data-ttu-id="3b5f6-264">Eventos de risco reativados contribuem no cálculo de nível de risco do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-264">Reactivated risk events contribute to the user risk level calculation.</span></span> <span data-ttu-id="3b5f6-265">Eventos de risco fechados por meio de correção (como redefinir uma senha de segurança) não podem ser reativados.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="3b5f6-266">**Para abrir o diálogo de configurações relacionadas**:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-266">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="3b5f6-267">Na folha **Azure AD Identity Protection**, em **Investigar**, clique em **Eventos de risco**.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-267">On the **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="3b5f6-268">![Redefinição de senha manual](./media/active-directory-identityprotection/1002.png "Redefinição de senha manual")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="3b5f6-269">Na lista **Eventos de risco** , clique em um risco.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-269">In the **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="3b5f6-270">![Redefinição de senha manual](./media/active-directory-identityprotection/1003.png "Redefinição de senha manual")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="3b5f6-271">Na folha de risco, clique com o botão direito do mouse em um usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-271">On the risk blade, right-click a user.</span></span>

    <span data-ttu-id="3b5f6-272">![Redefinição de senha manual](./media/active-directory-identityprotection/1004.png "Redefinição de senha manual")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="3b5f6-273">Fechar manualmente todos os eventos de risco para um usuário</span><span class="sxs-lookup"><span data-stu-id="3b5f6-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="3b5f6-274">Em vez de fechar manualmente os eventos de risco de um usuário de forma individual, o Azure Active Directory Identity Protection também fornece um método para fechar todos os eventos para um usuário com um clique.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method to close all events for a user with one click.</span></span>

<span data-ttu-id="3b5f6-275">![Ações](./media/active-directory-identityprotection/2222.png "Ações")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="3b5f6-276">Quando você clica em **Descartar todos os eventos**, todos os eventos são fechados e o usuário afetado não está mais em risco.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-276">When you click **Dismiss all events**, all events are closed and the affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="3b5f6-277">Corrigir eventos de risco do usuário</span><span class="sxs-lookup"><span data-stu-id="3b5f6-277">Remediating user risk events</span></span>

<span data-ttu-id="3b5f6-278">Uma correção é uma ação que visa proteger uma identidade ou um dispositivo que já sofreu comprometimento conhecido ou suspeito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-278">A remediation is an action to secure an identity or a device that was previously suspected or known to be compromised.</span></span> <span data-ttu-id="3b5f6-279">Uma correção restaura a identidade ou dispositivo para um estado seguro e resolve eventos de risco anteriores associados à identidade ou ao dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-279">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

<span data-ttu-id="3b5f6-280">Para corrigir os eventos de risco do usuário, você pode:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-280">To remediate user risk events, you can:</span></span>

* <span data-ttu-id="3b5f6-281">executar uma redefinição de senha de segurança para corrigir eventos de risco do usuário manualmente</span><span class="sxs-lookup"><span data-stu-id="3b5f6-281">Perform a secure password reset to remediate user risk events manually</span></span>
* <span data-ttu-id="3b5f6-282">configurar uma política de segurança de risco do usuário para mitigar ou corrigir eventos de risco do usuário automaticamente</span><span class="sxs-lookup"><span data-stu-id="3b5f6-282">Configure a user risk security policy to mitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="3b5f6-283">recriar imagem no dispositivo infectado</span><span class="sxs-lookup"><span data-stu-id="3b5f6-283">Re-image the infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="3b5f6-284">Redefinição de senha de segurança manual</span><span class="sxs-lookup"><span data-stu-id="3b5f6-284">Manual secure password reset</span></span>
<span data-ttu-id="3b5f6-285">Uma redefinição de senha de segurança é uma correção eficiente para muitos eventos de risco e quando executada, automaticamente fecha esses eventos de risco e recalcula o nível de risco do usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates the user risk level.</span></span> <span data-ttu-id="3b5f6-286">Você pode usar o painel do Identity Protection para iniciar uma redefinição de senha para um usuário arriscado.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-286">You can use the Identity Protection dashboard to initiate a password reset for a risky user.</span></span>

<span data-ttu-id="3b5f6-287">A caixa de diálogo correspondente fornece dois métodos diferentes para redefinir uma senha:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-287">The related dialog provides two different methods to reset a password:</span></span>

<span data-ttu-id="3b5f6-288">**Redefinir senha** - selecione **Exigir que o usuário redefina a senha** para permitir que o usuário se recupere automaticamente se ele estiver registrado para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-288">**Reset password** - Select **Require the user to reset their password** to allow the user to self-recover if the user has registered for multi-factor authentication.</span></span> <span data-ttu-id="3b5f6-289">Durante da próxima entrada do usuário, ele precisará resolver um desafio de autenticação multifator com êxito e em seguida, será forçado a alterar a senha.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-289">During the user's next sign-in, the user will be required to solve a multi-factor authentication challenge successfully and then, forced to change the password.</span></span> <span data-ttu-id="3b5f6-290">Essa opção não estará disponível se a conta de usuário não estiver registrada para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-290">This option isn't available if the user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="3b5f6-291">**Senha temporária** - selecione **Gerar uma senha temporária** para invalidar imediatamente a senha existente e criar uma nova senha temporária para o usuário.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-291">**Temporary password** - Select **Generate a temporary password** to immediately invalidate the existing password, and create a new temporary password for the user.</span></span> <span data-ttu-id="3b5f6-292">Envie a nova senha temporária para um endereço de email alternativo para o usuário ou para o gerente dele.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-292">Send the new temporary password to an alternate email address for the user or to the user's manager.</span></span> <span data-ttu-id="3b5f6-293">Como a senha é temporária, o usuário precisará alterá-la após entrar.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-293">Because the password is temporary, the user will be prompted to change the password upon sign-in.</span></span>

<span data-ttu-id="3b5f6-294">![Política](./media/active-directory-identityprotection/1005.png "Política")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="3b5f6-295">**Para abrir o diálogo de configurações relacionadas**:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-295">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="3b5f6-296">Na folha **Azure AD Identity Protection**, clique em **Usuários com riscos sinalizados**.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-296">On the **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="3b5f6-297">![Redefinição de senha manual](./media/active-directory-identityprotection/1006.png "Redefinição de senha manual")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="3b5f6-298">Na lista de usuários, selecione um usuário com eventos de pelo menos um risco.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-298">From the list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="3b5f6-299">![Redefinição de senha manual](./media/active-directory-identityprotection/1007.png "Redefinição de senha manual")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="3b5f6-300">Na folha de usuário, clique em **Redefinir senha**.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-300">On the user blade, click **Reset password**.</span></span>

    <span data-ttu-id="3b5f6-301">![Redefinição de senha manual](./media/active-directory-identityprotection/1008.png "Redefinição de senha manual")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="3b5f6-302">Política de segurança de risco do usuário</span><span class="sxs-lookup"><span data-stu-id="3b5f6-302">User risk security policy</span></span>
<span data-ttu-id="3b5f6-303">Uma política de segurança de risco do usuário é uma política de acesso condicional que avalia o nível de risco de um usuário específico e aplica ações de correção e mitigação com base em regras e condições predefinidas.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-303">A user risk security policy is a conditional access policy that evaluates the risk level to a specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="3b5f6-304">![Política do usuário ridk](./media/active-directory-identityprotection/1009.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="3b5f6-305">O Azure AD Identity Protection ajuda a gerenciar a mitigação e correção de usuários sinalizados para riscos, permitindo:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-305">Azure AD Identity Protection helps you manage the mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="3b5f6-306">Defina os usuários e os grupos aos quais a política se aplica:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-306">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="3b5f6-307">![Política do usuário ridk](./media/active-directory-identityprotection/1010.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="3b5f6-308">Defina o limite de nível de risco do usuário (baixo, médio ou alto) que dispara a política:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-308">Set the user risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="3b5f6-309">![Política do usuário ridk](./media/active-directory-identityprotection/1011.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="3b5f6-310">Defina os controles a serem impostos quando a política for disparada:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-310">Set the controls to be enforced when the policy triggers:</span></span>

    <span data-ttu-id="3b5f6-311">![Política do usuário ridk](./media/active-directory-identityprotection/1012.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="3b5f6-312">Alterne o estado de sua política:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-312">Switch the state of your policy:</span></span>

    <span data-ttu-id="3b5f6-313">![Política do usuário ridk](./media/active-directory-identityprotection/403.png "Registro de MFA")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="3b5f6-314">Examine e avalie o impacto de uma alteração antes de ativá-la:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-314">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="3b5f6-315">![Política do usuário ridk](./media/active-directory-identityprotection/1013.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="3b5f6-316">Escolher um limite **Alto** reduz o número de vezes que uma política é disparada e minimiza o impacto para os usuários.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-316">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>
<span data-ttu-id="3b5f6-317">No entanto, isso exclui usuários sinalizados com **Baixo** e **Médio** risco da política, o que pode não proteger as identidades ou os dispositivos que sofreram comprometimento conhecido ou suspeito.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-317">However, it excludes **Low** and **Medium** users flagged for risk from the policy, which may not secure identities or devices that were previously suspected or known to be compromised.</span></span>

<span data-ttu-id="3b5f6-318">Ao definir a política,</span><span class="sxs-lookup"><span data-stu-id="3b5f6-318">When setting the policy,</span></span>

* <span data-ttu-id="3b5f6-319">exclua os usuários que tendem a gerar muitos falsos positivos (desenvolvedores e analistas de segurança)</span><span class="sxs-lookup"><span data-stu-id="3b5f6-319">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="3b5f6-320">exclua os usuários em localidades em que não é viável habilitar a política (por exemplo, sem acesso à assistência técnica)</span><span class="sxs-lookup"><span data-stu-id="3b5f6-320">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="3b5f6-321">use um limite **Alto** durante a distribuição inicial de política ou se você precisar minimizar os desafios encontrados pelos usuários finais.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="3b5f6-322">use um limite **Baixo** se sua organização exigir uma segurança maior.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="3b5f6-323">Selecionar um limite **Baixo** apresenta desafios de entrada do usuário adicionais, porém representa uma segurança maior.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="3b5f6-324">O padrão recomendado na maioria das organizações é configurar uma regra para um limite **Médio** para atingir um equilíbrio entre segurança e usabilidade.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-324">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="3b5f6-325">Para obter uma visão geral da experiência do usuário relacionada, confira:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-325">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="3b5f6-326">[Fluxo de recuperação de conta comprometida](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="3b5f6-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="3b5f6-327">[Fluxo de conta comprometida bloqueada](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="3b5f6-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="3b5f6-328">**Para abrir o diálogo de configurações relacionadas**:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-328">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="3b5f6-329">Na folha **Azure AD Identity Protection**, na seção **Configurar**, clique em **Política de risco de usuário**.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-329">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="3b5f6-330">![Política do usuário ridk](./media/active-directory-identityprotection/1009.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="3b5f6-331">Mitigar eventos de risco do usuário</span><span class="sxs-lookup"><span data-stu-id="3b5f6-331">Mitigating user risk events</span></span>
<span data-ttu-id="3b5f6-332">Os administradores podem definir uma política de segurança de risco do usuário para bloquear os usuários ao entrar dependendo do nível de risco.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-332">Administrators can set a user risk security policy to block users upon sign-in depending on the risk level.</span></span>

<span data-ttu-id="3b5f6-333">Bloquear a entrada:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="3b5f6-334">impede a geração de novos eventos de risco do usuário para o usuário afetado</span><span class="sxs-lookup"><span data-stu-id="3b5f6-334">Prevents the generation of new user risk events for the affected user</span></span>
* <span data-ttu-id="3b5f6-335">Permite aos administradores corrigir os eventos de risco que afetam a identidade do usuário manualmente, bem como restaurá-la para um estado seguro</span><span class="sxs-lookup"><span data-stu-id="3b5f6-335">Enables administrators to manually remediate the risk events affecting the user's identity and restore it to a secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="3b5f6-336">Política de registro de autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="3b5f6-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="3b5f6-337">A autenticação multifator do Azure é um método de verificar quem você é e que requer o uso de mais do que apenas um nome de usuário e uma senha.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-337">Azure multi-factor authentication is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="3b5f6-338">Ele fornece uma segunda camada de segurança para logons de usuário e transações.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-338">It provides a second layer of security to user sign-ins and transactions.</span></span>  
<span data-ttu-id="3b5f6-339">Recomendamos exigir a autenticação multifator do Azure para entradas de usuário porque:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="3b5f6-340">fornece autenticação forte com uma variedade de opções de verificação fácil</span><span class="sxs-lookup"><span data-stu-id="3b5f6-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="3b5f6-341">desempenha um papel fundamental na preparação de sua organização para proteger e recuperar comprometimentos de conta</span><span class="sxs-lookup"><span data-stu-id="3b5f6-341">Plays a key role in preparing your organization to protect and recover from account compromises</span></span>

<span data-ttu-id="3b5f6-342">![Política do usuário ridk](./media/active-directory-identityprotection/1019.png "Política do usuário ridk")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="3b5f6-343">Para obter mais detalhes, veja [O que é o Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3b5f6-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="3b5f6-344">O Azure AD Identity Protection ajuda a gerenciar a implementação do registro de autenticação multifator configurando uma política que permite:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-344">Azure AD Identity Protection helps you manage the roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="3b5f6-345">Defina os usuários e os grupos aos quais a política se aplica:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-345">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="3b5f6-346">![Política de MFA](./media/active-directory-identityprotection/1020.png "Política de MFA")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="3b5f6-347">Defina os controles a serem impostos quando a política for disparada:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-347">Set the controls to be enforced when the policy triggers::</span></span>  

    <span data-ttu-id="3b5f6-348">![Política de MFA](./media/active-directory-identityprotection/1021.png "Política de MFA")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="3b5f6-349">Alterne o estado de sua política:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-349">Switch the state of your policy:</span></span>

    <span data-ttu-id="3b5f6-350">![Política de MFA](./media/active-directory-identityprotection/403.png "Política de MFA")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="3b5f6-351">Exiba o status atual do registro:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-351">View the current registration status:</span></span>

    <span data-ttu-id="3b5f6-352">![Política de MFA](./media/active-directory-identityprotection/1022.png "Política de MFA")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="3b5f6-353">Para obter uma visão geral da experiência do usuário relacionada, confira:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-353">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="3b5f6-354">[Fluxo do registro de autenticação multifator](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="3b5f6-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="3b5f6-355">[Experiências de entrada com o Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="3b5f6-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="3b5f6-356">**Para abrir o diálogo de configurações relacionadas**:</span><span class="sxs-lookup"><span data-stu-id="3b5f6-356">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="3b5f6-357">Na folha **Azure AD Identity Protection**, na seção **Configurar**, clique em **Registro de autenticação multifator**.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-357">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="3b5f6-358">![Política de MFA](./media/active-directory-identityprotection/1019.png "Política de MFA")</span><span class="sxs-lookup"><span data-stu-id="3b5f6-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b5f6-359">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3b5f6-359">Next steps</span></span>
* [<span data-ttu-id="3b5f6-360">Canal 9: Azure AD e Identity Show: visualização do Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3b5f6-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="3b5f6-361">Habilitando o Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3b5f6-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="3b5f6-362">Vulnerabilidades detectadas pelo Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3b5f6-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="3b5f6-363">Eventos de risco do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3b5f6-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="3b5f6-364">Notificações do Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3b5f6-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="3b5f6-365">Guia estratégico do Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3b5f6-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="3b5f6-366">Glossário do Azure Active Directory Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="3b5f6-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="3b5f6-367">Experiências de entrada com o Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3b5f6-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="3b5f6-368">Azure Active Directory Identity Protection - como desbloquear usuários</span><span class="sxs-lookup"><span data-stu-id="3b5f6-368">Azure Active Directory Identity Protection - How to unblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="3b5f6-369">Introdução ao Azure Active Directory Identity Protection e ao Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="3b5f6-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
