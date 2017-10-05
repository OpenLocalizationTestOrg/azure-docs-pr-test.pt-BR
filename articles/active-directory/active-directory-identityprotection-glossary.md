---
title: "Glossário do Azure Active Directory Identity Protection | Microsoft Docs"
description: "Glossário do Azure Active Directory Identity Protection"
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gerenciamento de aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança, glossário"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 2cf64925cff9a78cf83532a1cfd231f7a1d98304
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a><span data-ttu-id="e2809-104">Glossário do Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e2809-104">Azure Active Directory Identity Protection Glossary</span></span>
### <a name="at-risk-user"></a><span data-ttu-id="e2809-105">Em risco (Usuário)</span><span class="sxs-lookup"><span data-stu-id="e2809-105">At risk (User)</span></span>
<span data-ttu-id="e2809-106">Um usuário com um ou mais eventos de risco ativos.</span><span class="sxs-lookup"><span data-stu-id="e2809-106">A user with one or more active risk events.</span></span> 

### <a name="atypical-sign-in-location"></a><span data-ttu-id="e2809-107">Local de entrada atípico</span><span class="sxs-lookup"><span data-stu-id="e2809-107">Atypical sign-in location</span></span>
<span data-ttu-id="e2809-108">Uma entrada de um local geográfico incomum para o usuário específico, usuários semelhantes ou o locatário.</span><span class="sxs-lookup"><span data-stu-id="e2809-108">A sign-in from a geographic location that is not typical for the specific user, similar users, or the tenant.</span></span>

### <a name="azure-ad-identity-protection"></a><span data-ttu-id="e2809-109">Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e2809-109">Azure AD Identity Protection</span></span>
<span data-ttu-id="e2809-110">Um módulo de segurança do Azure Active Directory que fornece uma exibição consolidada dos eventos de risco e das possíveis vulnerabilidades que afetam as identidades de uma organização.</span><span class="sxs-lookup"><span data-stu-id="e2809-110">A security module of Azure Active Directory that provides a consolidated view into risk events and potential vulnerabilities affecting an organization’s identities.</span></span>

### <a name="conditional-access"></a><span data-ttu-id="e2809-111">Acesso condicional</span><span class="sxs-lookup"><span data-stu-id="e2809-111">Conditional access</span></span>
<span data-ttu-id="e2809-112">Uma política para proteger o acesso aos recursos.</span><span class="sxs-lookup"><span data-stu-id="e2809-112">A policy for securing access to resources.</span></span> <span data-ttu-id="e2809-113">Regras de acesso condicional são armazenadas no Azure Active Directory e são avaliadas pelo Azure AD antes de conceder acesso ao recurso.</span><span class="sxs-lookup"><span data-stu-id="e2809-113">Conditional access rules are stored in the Azure Active Directory and are evaluated by Azure AD before granting access to the resource.</span></span>  <span data-ttu-id="e2809-114">As regras de exemplo incluem restrição baseada na localização do usuário, integridade do dispositivo ou método de autenticação do usuário.</span><span class="sxs-lookup"><span data-stu-id="e2809-114">Example rules include restricting access based on user location, device health or user authentication method.</span></span>

### <a name="credentials"></a><span data-ttu-id="e2809-115">Credenciais</span><span class="sxs-lookup"><span data-stu-id="e2809-115">Credentials</span></span>
<span data-ttu-id="e2809-116">Informações que incluem a identificação e prova de identificação usadas para obter acesso ao local e aos recursos da rede.</span><span class="sxs-lookup"><span data-stu-id="e2809-116">Information that includes identification and proof of identification that is used to gain access to local and network resources.</span></span> <span data-ttu-id="e2809-117">Exemplos de credenciais são nomes de usuário e senhas, cartões inteligentes e certificados.</span><span class="sxs-lookup"><span data-stu-id="e2809-117">Examples of credentials are user names and passwords, smart cards, and certificates.</span></span>

### <a name="event"></a><span data-ttu-id="e2809-118">Evento</span><span class="sxs-lookup"><span data-stu-id="e2809-118">Event</span></span>
<span data-ttu-id="e2809-119">Um registro de uma atividade no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2809-119">A record of an activity in Azure Active Directory.</span></span>

### <a name="false-positive-risk-event"></a><span data-ttu-id="e2809-120">Falsos positivos (evento de risco)</span><span class="sxs-lookup"><span data-stu-id="e2809-120">False-positive (risk event)</span></span>
<span data-ttu-id="e2809-121">Um status de evento de risco definido manualmente por um usuário do Identity Protection que indica que o evento foi investigado e foi marcado incorretamente como um evento de risco.</span><span class="sxs-lookup"><span data-stu-id="e2809-121">A risk event status set manually by an Identity Protection user, indicating that the risk event was investigated and was incorrectly flagged as a risk event.</span></span>

### <a name="identity"></a><span data-ttu-id="e2809-122">Identidade</span><span class="sxs-lookup"><span data-stu-id="e2809-122">Identity</span></span>
<span data-ttu-id="e2809-123">Uma pessoa ou entidade que deve ser verificada por meio de autenticação com base em critérios como senha ou certificado.</span><span class="sxs-lookup"><span data-stu-id="e2809-123">A person or entity that must be verified by means of authentication, based on criteria such as password or a certificate.</span></span>

### <a name="identity-risk-event"></a><span data-ttu-id="e2809-124">Evento de risco de identidade</span><span class="sxs-lookup"><span data-stu-id="e2809-124">Identity risk event</span></span>
<span data-ttu-id="e2809-125">Um evento AAD que foi marcado como anômalo pelo Identity Protection e pode indicar que uma identidade foi comprometida.</span><span class="sxs-lookup"><span data-stu-id="e2809-125">AAD event that was flagged as anomalous by Identity Protection, and may indicate that an identity has been compromised.</span></span>

### <a name="ignored-risk-event"></a><span data-ttu-id="e2809-126">Ignorado (evento de risco)</span><span class="sxs-lookup"><span data-stu-id="e2809-126">Ignored (risk event)</span></span>
<span data-ttu-id="e2809-127">Um status de evento de risco definido manualmente por um usuário do Identity Protection que indica que o evento foi fechado sem realizar uma ação de correção.</span><span class="sxs-lookup"><span data-stu-id="e2809-127">A risk event status set manually by an Identity Protection user, indicating that the risk event is closed without taking a remediation action.</span></span>

### <a name="impossible-travel-from-atypical-locations"></a><span data-ttu-id="e2809-128">Viagem impossível de locais atípicos</span><span class="sxs-lookup"><span data-stu-id="e2809-128">Impossible travel from atypical locations</span></span>
<span data-ttu-id="e2809-129">Um evento de risco disparado quando duas entradas para o mesmo usuário são detectadas, sendo pelo menos uma delas de um local de entrada atípico e em que o tempo entre as entradas é menor do que o tempo mínimo necessário para viajar fisicamente entre esses locais.</span><span class="sxs-lookup"><span data-stu-id="e2809-129">A risk event triggered when two sign-ins for the same user are detected, where at least one of them is from an atypical sign-in location, and where the time between the sign-ins is shorter than the minimum time it would take to physically travel between these locations.</span></span>  

### <a name="investigation"></a><span data-ttu-id="e2809-130">Investigação</span><span class="sxs-lookup"><span data-stu-id="e2809-130">Investigation</span></span>
<span data-ttu-id="e2809-131">O processo de revisão de atividades, logs e outras informações relevantes relacionadas a um evento de risco para decidir se as etapas de correção e mitigação são necessárias, como a identidade foi comprometida e entender como ela foi usada.</span><span class="sxs-lookup"><span data-stu-id="e2809-131">The process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary, understand if and how the identity was compromised, and understand how the compromised identity was used.</span></span>

### <a name="leaked-credentials"></a><span data-ttu-id="e2809-132">Credenciais vazadas</span><span class="sxs-lookup"><span data-stu-id="e2809-132">Leaked credentials</span></span>
<span data-ttu-id="e2809-133">Um evento de risco disparado quando as credenciais do usuário atual (nome de usuário e senha) são encontradas como postadas publicamente por nossos pesquisadores na Dark Web.</span><span class="sxs-lookup"><span data-stu-id="e2809-133">A risk event triggered when current user credentials (user name and password) are found posted publicly in the Dark   web by our researchers.</span></span>

### <a name="mitigation"></a><span data-ttu-id="e2809-134">Redução</span><span class="sxs-lookup"><span data-stu-id="e2809-134">Mitigation</span></span>
<span data-ttu-id="e2809-135">Uma ação que visa limitar ou eliminar a capacidade de um invasor explorar uma identidade ou um dispositivo comprometidos sem restaurá-los para um estado seguro.</span><span class="sxs-lookup"><span data-stu-id="e2809-135">An action to limit or eliminate the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="e2809-136">Uma mitigação não resolve eventos de risco anteriores associados à identidade ou ao dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e2809-136">A mitigation does not resolve previous risk events associated with the identity or device.</span></span>

### <a name="multi-factor-authentication"></a><span data-ttu-id="e2809-137">Autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="e2809-137">Multi-factor authentication</span></span>
<span data-ttu-id="e2809-138">Um método de autenticação que exige dois ou mais métodos de autenticação, que podem incluir algo que o usuário tem, como um certificado; algo que o usuário conhece, como nomes de usuário, senhas ou frases secretas; atributos físicos, como uma impressão digital; e atributos pessoais, como uma assinatura pessoal.</span><span class="sxs-lookup"><span data-stu-id="e2809-138">An authentication method that requires two or more authentication methods, which may include something the user has, such a certificate; something the user knows, such as user names, passwords, or pass phrases; physical attributes, such as a thumbprint; and personal attributes, such as a personal signature.</span></span>

### <a name="offline-detection"></a><span data-ttu-id="e2809-139">Detecção offline</span><span class="sxs-lookup"><span data-stu-id="e2809-139">Offline detection</span></span>
<span data-ttu-id="e2809-140">A detecção de anomalias e a avaliação do risco de um evento, tal como uma tentativa de entrada após o ocorrido, para um evento que já aconteceu.</span><span class="sxs-lookup"><span data-stu-id="e2809-140">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt after the fact, for an event that has already happened.</span></span>

### <a name="policy-condition"></a><span data-ttu-id="e2809-141">Condição da política</span><span class="sxs-lookup"><span data-stu-id="e2809-141">Policy condition</span></span>
<span data-ttu-id="e2809-142">Uma parte de uma política de segurança que define as entidades (grupos, usuários, aplicativos, plataformas de dispositivos, Estados de dispositivo, intervalos de IP e tipos de cliente) incluídas na política ou excluídas dela.</span><span class="sxs-lookup"><span data-stu-id="e2809-142">A part of a security policy which defines the entities (groups, users, apps, device platforms, Device states, IP ranges, client types) included in the policy or excluded from it.</span></span>

### <a name="policy-rule"></a><span data-ttu-id="e2809-143">Regra de política</span><span class="sxs-lookup"><span data-stu-id="e2809-143">Policy rule</span></span>
<span data-ttu-id="e2809-144">A parte de uma política de segurança que descreve as circunstâncias que vai disparar a política e as ações executadas quando ela é acionada.</span><span class="sxs-lookup"><span data-stu-id="e2809-144">The part of a security policy which describes the circumstances that would trigger the policy, and the actions taken when the policy is triggered.</span></span>

### <a name="prevention"></a><span data-ttu-id="e2809-145">Prevenção</span><span class="sxs-lookup"><span data-stu-id="e2809-145">Prevention</span></span>
<span data-ttu-id="e2809-146">Uma ação para evitar danos à organização por abuso de uma identidade ou dispositivo que sofreu comprometimento conhecido ou suspeito.</span><span class="sxs-lookup"><span data-stu-id="e2809-146">An action to prevent damage to the organization through abuse of an identity or device suspected or know to be compromised.</span></span> <span data-ttu-id="e2809-147">Uma ação de prevenção não protege o dispositivo ou a identidade, e não resolve eventos de risco anteriores.</span><span class="sxs-lookup"><span data-stu-id="e2809-147">A prevention action does not secure the device or identity, and does not resolve previous risk events.</span></span>

### <a name="privileged-user"></a><span data-ttu-id="e2809-148">Privilegiado (usuário)</span><span class="sxs-lookup"><span data-stu-id="e2809-148">Privileged (user)</span></span>
<span data-ttu-id="e2809-149">Um usuário que, no momento de um evento de risco, tinha permissões de administrador permanentes ou temporárias a um ou mais recursos no Azure Active Directory, como um Administrador Global, Administrador de Cobrança, Administrador de Serviços, Administrador de Usuários e Administrador de Senha.</span><span class="sxs-lookup"><span data-stu-id="e2809-149">A user that at the time of a risk event, had permanent or temporary admin permissions to one or more resource in Azure Active Directory, such as a Global Administrator, Billing Administrator, Service Administrator, User administrator, and Password Administrator.</span></span> 

### <a name="real-time"></a><span data-ttu-id="e2809-150">Tempo real</span><span class="sxs-lookup"><span data-stu-id="e2809-150">Real-time</span></span>
<span data-ttu-id="e2809-151">Consulte Detecção em tempo real.</span><span class="sxs-lookup"><span data-stu-id="e2809-151">See Real-time detection.</span></span>

### <a name="real-time-detection"></a><span data-ttu-id="e2809-152">Detecção em tempo real.</span><span class="sxs-lookup"><span data-stu-id="e2809-152">Real-time detection</span></span>
<span data-ttu-id="e2809-153">A detecção de anomalias e a avaliação do risco de um evento, tal como uma tentativa de entrada antes de permitir que o evento prossiga.</span><span class="sxs-lookup"><span data-stu-id="e2809-153">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt before the event is allowed to proceed.</span></span>

### <a name="remediated-risk-event"></a><span data-ttu-id="e2809-154">Corrigido (evento de risco)</span><span class="sxs-lookup"><span data-stu-id="e2809-154">Remediated (risk event)</span></span>
<span data-ttu-id="e2809-155">Um status de evento de risco definido automaticamente pelo Identity Protection, que indica que o evento foi corrigido usando a ação de correção padrão para esse tipo de evento de risco.</span><span class="sxs-lookup"><span data-stu-id="e2809-155">A risk event status set automatically by Identity Protection, indicating that the risk event was remediated using the standard remediation action for this type of risk event.</span></span> <span data-ttu-id="e2809-156">Por exemplo, quando a senha do usuário é redefinida, muitos eventos de risco que indicam que a senha anterior foi comprometida são corrigidos automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e2809-156">For example, when the user password is reset, many risk events that indicate that the previous password was compromised are automatically remediated.</span></span>

### <a name="remediation"></a><span data-ttu-id="e2809-157">Correção</span><span class="sxs-lookup"><span data-stu-id="e2809-157">Remediation</span></span>
<span data-ttu-id="e2809-158">Uma ação que visa proteger uma identidade ou um dispositivo que sofreu comprometimento conhecido ou suspeito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e2809-158">An action to secure an identity or a device that were previously suspected or known to be compromised.</span></span> <span data-ttu-id="e2809-159">Uma correção restaura a identidade ou dispositivo para um estado seguro e resolve eventos de risco anteriores associados à identidade ou ao dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e2809-159">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

### <a name="resolved-risk-event"></a><span data-ttu-id="e2809-160">Resolvido (evento de risco)</span><span class="sxs-lookup"><span data-stu-id="e2809-160">Resolved (risk event)</span></span>
<span data-ttu-id="e2809-161">Um status de evento de risco definido manualmente por um usuário do Identity Protection que indica que o usuário executou uma ação de correção apropriada fora do Identity Protection e que o evento deve ser considerado fechado.</span><span class="sxs-lookup"><span data-stu-id="e2809-161">A risk event status set manually by an Identity Protection user, indicating that the user took an appropriate remediation action outside Identity Protection, and that the risk event should be considered closed.</span></span>

### <a name="risk-event-status"></a><span data-ttu-id="e2809-162">Status de evento de risco</span><span class="sxs-lookup"><span data-stu-id="e2809-162">Risk event status</span></span>
<span data-ttu-id="e2809-163">Uma propriedade de um evento de risco que indica se o evento está ativo e, se fechado, o motivo para estar fechado.</span><span class="sxs-lookup"><span data-stu-id="e2809-163">A property of a risk event, indicating whether the event is active, and if closed, the reason for closing it.</span></span>

### <a name="risk-event-type"></a><span data-ttu-id="e2809-164">Tipo de evento de risco</span><span class="sxs-lookup"><span data-stu-id="e2809-164">Risk event type</span></span>
<span data-ttu-id="e2809-165">Uma categoria para o evento de risco que indica o tipo de anomalia que fez com que o evento fosse considerado arriscado.</span><span class="sxs-lookup"><span data-stu-id="e2809-165">A category for the risk event, indicating the type of anomaly that caused the event to be considered risky.</span></span>

### <a name="risk-level-risk-event"></a><span data-ttu-id="e2809-166">Nível de risco (evento de risco)</span><span class="sxs-lookup"><span data-stu-id="e2809-166">Risk level (risk event)</span></span>
<span data-ttu-id="e2809-167">Uma indicação (Alta, Média ou Baixa) da severidade do evento de risco para ajudar os usuários do Identity Protection a priorizar as ações tomadas para reduzir o risco para a organização.</span><span class="sxs-lookup"><span data-stu-id="e2809-167">An indication (High, Medium, or Low) of the severity of the risk event to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span></span> 

### <a name="risk-level-sign-in"></a><span data-ttu-id="e2809-168">Nível de risco (entrada)</span><span class="sxs-lookup"><span data-stu-id="e2809-168">Risk level (sign-in)</span></span>
<span data-ttu-id="e2809-169">Uma indicação (Alta, Média ou Baixa) da probabilidade de que outra pessoa esteja tentando usar a identidade do usuário para uma entrada específica.</span><span class="sxs-lookup"><span data-stu-id="e2809-169">An indication (High, Medium, or Low) of the likelihood that for a specific sign-in, someone else is attempting to use the user’s identity.</span></span>

### <a name="risk-level-user-compromise"></a><span data-ttu-id="e2809-170">Nível de risco (comprometimento do usuário)</span><span class="sxs-lookup"><span data-stu-id="e2809-170">Risk level (user compromise)</span></span>
<span data-ttu-id="e2809-171">Uma indicação (Alta, Média ou Baixa) da probabilidade de uma identidade ter sido comprometida.</span><span class="sxs-lookup"><span data-stu-id="e2809-171">An indication (High, Medium, or Low) of the likelihood that an identity has been compromised.</span></span>

### <a name="risk-level-vulnerability"></a><span data-ttu-id="e2809-172">Nível de risco (vulnerabilidade)</span><span class="sxs-lookup"><span data-stu-id="e2809-172">Risk level (vulnerability)</span></span>
<span data-ttu-id="e2809-173">Uma indicação (Alta, Média ou Baixa) da severidade da vulnerabilidade para ajudar os usuários do Identity Protection a priorizar as ações tomadas para reduzir o risco para a organização.</span><span class="sxs-lookup"><span data-stu-id="e2809-173">An indication (High, Medium, or Low) of the severity of the vulnerability to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span></span>

### <a name="secure-identity"></a><span data-ttu-id="e2809-174">Proteger (identidade)</span><span class="sxs-lookup"><span data-stu-id="e2809-174">Secure (identity)</span></span>
<span data-ttu-id="e2809-175">Realizar uma ação de correção como uma alteração de senha ou reimplantação da imagem no computador para restaurar uma identidade potencialmente comprometida para um estado não comprometido.</span><span class="sxs-lookup"><span data-stu-id="e2809-175">Take remediation action such as a password change or machine reimaging to restore a potentially compromised identity to an uncompromised state.</span></span>

### <a name="security-policy"></a><span data-ttu-id="e2809-176">Política de segurança</span><span class="sxs-lookup"><span data-stu-id="e2809-176">Security policy</span></span>
<span data-ttu-id="e2809-177">Uma coleção de regras e condição da política.</span><span class="sxs-lookup"><span data-stu-id="e2809-177">A collection of policy rules and condition.</span></span> <span data-ttu-id="e2809-178">Uma política pode ser aplicada a entidades como usuários, grupos, aplicativos, dispositivos, plataformas de dispositivos, estados de dispositivo, intervalos de IP e tipos de cliente do Auth2.0.</span><span class="sxs-lookup"><span data-stu-id="e2809-178">A policy can be applied to entities such as users, groups, apps, devices, device platforms, device states, IP ranges, and Auth2.0 client types.</span></span> <span data-ttu-id="e2809-179">Quando uma política está habilitada, ela é avaliada sempre que um token para um recurso é emitido para uma entidade incluída na política.</span><span class="sxs-lookup"><span data-stu-id="e2809-179">When a policy is enabled, it is evaluated whenever an entity included in the policy is issued a token for a resource.</span></span>

### <a name="sign-in-v"></a><span data-ttu-id="e2809-180">Entrar (v)</span><span class="sxs-lookup"><span data-stu-id="e2809-180">Sign in (v)</span></span>
<span data-ttu-id="e2809-181">Autenticar-se em uma identidade no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2809-181">To authenticate to an identity in Azure Active Directory.</span></span>

### <a name="sign-in-n"></a><span data-ttu-id="e2809-182">Entrada (n)</span><span class="sxs-lookup"><span data-stu-id="e2809-182">Sign-in (n)</span></span>
<span data-ttu-id="e2809-183">O processo ou a ação de autenticar uma identidade no Azure Active Directory e o evento que captura essa operação.</span><span class="sxs-lookup"><span data-stu-id="e2809-183">The process or action of authenticating an identity in Azure Active Directory, and the event that captures this operation.</span></span>

### <a name="sign-in-from-anonymous-ip-address"></a><span data-ttu-id="e2809-184">Entrada de um endereço IP anônimo</span><span class="sxs-lookup"><span data-stu-id="e2809-184">Sign-in from anonymous IP address</span></span>
<span data-ttu-id="e2809-185">Um evento de risco disparado após uma entrada bem-sucedida de um endereço IP que foi identificado como um endereço IP de proxy anônimo.</span><span class="sxs-lookup"><span data-stu-id="e2809-185">A risk event triggered after a successful sign-in from IP address that has been identified as an anonymous proxy IP address.</span></span>

### <a name="sign-in-from-infected-device"></a><span data-ttu-id="e2809-186">Entradas de um dispositivo infectado</span><span class="sxs-lookup"><span data-stu-id="e2809-186">Sign-in from infected device</span></span>
<span data-ttu-id="e2809-187">Um evento de risco disparado em que uma entrada origina um endereço IP conhecido por ser usado por um ou mais dispositivos comprometidos, que estão tentando ativamente comunicar-se com um servidor de bot.</span><span class="sxs-lookup"><span data-stu-id="e2809-187">A risk event triggered when a sign-in originates from an IP address which is known to be used by one or more compromised devices, which are actively attempting to communicate with a bot server.</span></span>

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a><span data-ttu-id="e2809-188">Entrada de um endereço IP com atividade suspeita</span><span class="sxs-lookup"><span data-stu-id="e2809-188">Sign-in from IP address with suspicious activity</span></span>
<span data-ttu-id="e2809-189">Um evento de risco acionado depois de uma entrada bem-sucedida de um endereço IP com um grande número de tentativas de logon com falha em várias contas de usuário em um curto período de tempo.</span><span class="sxs-lookup"><span data-stu-id="e2809-189">A risk event triggered after a successful sign-in from an IP address with a high number of failed login attempts across multiple user accounts over a short period of time.</span></span>

### <a name="sign-in-from-unfamiliar-location"></a><span data-ttu-id="e2809-190">Entrada de um local desconhecido</span><span class="sxs-lookup"><span data-stu-id="e2809-190">Sign-in from unfamiliar location</span></span>
<span data-ttu-id="e2809-191">Um evento de risco disparado quando um usuário entra com êxito de um novo local (IP, Latitude/Longitude e ASN).</span><span class="sxs-lookup"><span data-stu-id="e2809-191">A risk event triggered when a user successfully signs in from a new location (IP, Latitude/Longitude and ASN).</span></span>

### <a name="sign-in-risk"></a><span data-ttu-id="e2809-192">Risco de entrada</span><span class="sxs-lookup"><span data-stu-id="e2809-192">Sign-in risk</span></span>
<span data-ttu-id="e2809-193">Consulte Nível de risco (entrada)</span><span class="sxs-lookup"><span data-stu-id="e2809-193">See Risk level (sign-in)</span></span>

### <a name="sign-in-risk-policy"></a><span data-ttu-id="e2809-194">Política de risco de entrada</span><span class="sxs-lookup"><span data-stu-id="e2809-194">Sign-in risk policy</span></span>
<span data-ttu-id="e2809-195">Uma política de acesso condicional que avalia o risco de uma entrada específica e aplica mitigações com base em regras e condições predefinidas.</span><span class="sxs-lookup"><span data-stu-id="e2809-195">A conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="user-compromise-risk"></a><span data-ttu-id="e2809-196">Risco de comprometimento do usuário</span><span class="sxs-lookup"><span data-stu-id="e2809-196">User compromise risk</span></span>
<span data-ttu-id="e2809-197">Consulte Nível de risco (comprometimento do usuário)</span><span class="sxs-lookup"><span data-stu-id="e2809-197">See Risk level (user compromise)</span></span>

### <a name="user-risk"></a><span data-ttu-id="e2809-198">Risco do usuário</span><span class="sxs-lookup"><span data-stu-id="e2809-198">User risk</span></span>
<span data-ttu-id="e2809-199">Consulte Nível de risco (comprometimento do usuário).</span><span class="sxs-lookup"><span data-stu-id="e2809-199">See Risk level (user compromise).</span></span>

### <a name="user-risk-policy"></a><span data-ttu-id="e2809-200">Política de risco do usuário</span><span class="sxs-lookup"><span data-stu-id="e2809-200">User risk policy</span></span>
<span data-ttu-id="e2809-201">Uma política de acesso condicional que considera a entrada e aplica mitigações com base em regras e condições predefinidas.</span><span class="sxs-lookup"><span data-stu-id="e2809-201">A conditional access policy that considers the sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="users-flagged-for-risk"></a><span data-ttu-id="e2809-202">Usuários sinalizados por risco</span><span class="sxs-lookup"><span data-stu-id="e2809-202">Users flagged for risk</span></span>
<span data-ttu-id="e2809-203">Usuários que têm eventos de risco ativos ou corrigidos</span><span class="sxs-lookup"><span data-stu-id="e2809-203">Users that have risk events which are either active or remediated</span></span>

### <a name="vulnerability"></a><span data-ttu-id="e2809-204">Vulnerabilidade</span><span class="sxs-lookup"><span data-stu-id="e2809-204">Vulnerability</span></span>
<span data-ttu-id="e2809-205">Uma configuração ou condição no Azure Active Directory que torna o diretório suscetível a vulnerabilidades e ameaças.</span><span class="sxs-lookup"><span data-stu-id="e2809-205">A configuration or condition in Azure Active Directory which makes the directory susceptible to exploits or threats.</span></span>

## <a name="see-also"></a><span data-ttu-id="e2809-206">Confira também</span><span class="sxs-lookup"><span data-stu-id="e2809-206">See also</span></span>
* [<span data-ttu-id="e2809-207">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e2809-207">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

