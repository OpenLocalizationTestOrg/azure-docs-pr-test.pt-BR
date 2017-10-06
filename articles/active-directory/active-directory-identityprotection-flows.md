---
title: "experiências de aaaSign com o Azure AD Identity Protection | Microsoft Docs"
description: "Fornece uma visão geral da experiência do usuário hello quando Identity Protection tem atenuados ou corrigida, um usuário ou quando a autenticação multifator é necessária por uma política."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gerenciamento de aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="b1bbb-104">Experiências de entrada com a proteção de identidade do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1bbb-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="b1bbb-105">Com o Azure Active Directory Identity Protection, é possível:</span><span class="sxs-lookup"><span data-stu-id="b1bbb-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="b1bbb-106">Exigir usuários tooregister para autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="b1bbb-106">require users tooregister for multi-factor authentication</span></span>
* <span data-ttu-id="b1bbb-107">lidar com entradas arriscadas e usuários comprometidos</span><span class="sxs-lookup"><span data-stu-id="b1bbb-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="b1bbb-108">resposta de Olá Olá toothese dos problemas do sistema tem um impacto na experiência de logon do usuário, porque apenas diretamente entrando fornecendo um nome de usuário e uma senha não será possível mais.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-108">hello response of hello system toothese issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="b1bbb-109">Etapas adicionais serão necessária tooget um usuário de volta com segurança aos negócios.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-109">Additional steps are required tooget a user safely back into business.</span></span>

<span data-ttu-id="b1bbb-110">Este tópico fornece uma visão geral da experiência de entrada de um usuário em relação a todos os casos que podem ocorrer.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="b1bbb-111">**Autenticação multifator**</span><span class="sxs-lookup"><span data-stu-id="b1bbb-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="b1bbb-112">Registro de autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="b1bbb-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="b1bbb-113">**Entrada em risco**</span><span class="sxs-lookup"><span data-stu-id="b1bbb-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="b1bbb-114">Recuperação de entrada arriscada</span><span class="sxs-lookup"><span data-stu-id="b1bbb-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="b1bbb-115">Entrada arriscada bloqueada</span><span class="sxs-lookup"><span data-stu-id="b1bbb-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="b1bbb-116">Registro da autenticação multifator durante a entrada arriscada</span><span class="sxs-lookup"><span data-stu-id="b1bbb-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="b1bbb-117">**Usuário em risco**</span><span class="sxs-lookup"><span data-stu-id="b1bbb-117">**User at risk**</span></span>

* <span data-ttu-id="b1bbb-118">Recuperação de conta comprometida</span><span class="sxs-lookup"><span data-stu-id="b1bbb-118">Compromised account recovery</span></span>
* <span data-ttu-id="b1bbb-119">Conta comprometida bloqueada</span><span class="sxs-lookup"><span data-stu-id="b1bbb-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="b1bbb-120">Registro de autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="b1bbb-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="b1bbb-121">Olá melhor experiência de usuário para ambos, Olá fluxo de recuperação de conta comprometida e Olá arriscado fluxo de entrada, é quando o usuário Olá pode recuperar automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-121">hello best user experience for both, hello compromised account recovery flow and hello risky sign-in flow, is when hello user can self-recover.</span></span> <span data-ttu-id="b1bbb-122">Se os usuários são registrados para autenticação multifator, eles já tem um número de telefone associado à conta que pode ser usado toopass desafios de segurança.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used toopass security challenges.</span></span> <span data-ttu-id="b1bbb-123">Nenhum envolvimento de Ajuda do suporte técnico ou administrador é necessário toorecover contra o comprometimento de conta.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-123">No help desk or administrator involvement is needed toorecover from account compromise.</span></span> <span data-ttu-id="b1bbb-124">Assim, é altamente recomendável tooget aos usuários registrados para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-124">Thus, it’s highly recommended tooget your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="b1bbb-125">Os administradores podem:</span><span class="sxs-lookup"><span data-stu-id="b1bbb-125">Administrators can:</span></span>

* <span data-ttu-id="b1bbb-126">Defina uma política que exige que usuários tooset suas contas de verificação de segurança adicional.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-126">set a policy that requires users tooset up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="b1bbb-127">Permitir ignorar o registro de autenticação multifator para backup too30 dias, no caso de desejarem toogive usuários antes de registrar um período de cortesia.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-127">allow skipping multi-factor authentication registration for up too30 days, in case they want toogive users a grace period before registering.</span></span>

<span data-ttu-id="b1bbb-128">**registro de autenticação multifator Olá tem três etapas:**</span><span class="sxs-lookup"><span data-stu-id="b1bbb-128">**hello multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="b1bbb-129">Na primeira etapa de hello, usuário Olá recebe uma notificação sobre a conta de saudação do hello requisito tooset para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-129">In hello first step, hello user gets a notification about hello requirement tooset hello account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="b1bbb-130">![Correção](./media/active-directory-identityprotection-flows/140.png "Correção")</span><span class="sxs-lookup"><span data-stu-id="b1bbb-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="b1bbb-131">autenticação de multifator tooset backup, é necessário que o sistema de saudação do toolet Saiba como você deseja toobe contatado.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-131">tooset multi-factor authentication up, you need toolet hello system know how you want toobe contacted.</span></span>
   
    <span data-ttu-id="b1bbb-132">![Correção](./media/active-directory-identityprotection-flows/141.png "Correção")</span><span class="sxs-lookup"><span data-stu-id="b1bbb-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="b1bbb-133">sistema Olá envia um desafio tooyou e precisar toorespond.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-133">hello system submits a challenge tooyou and you need toorespond.</span></span>
   
    <span data-ttu-id="b1bbb-134">![Correção](./media/active-directory-identityprotection-flows/142.png "Correção")</span><span class="sxs-lookup"><span data-stu-id="b1bbb-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="b1bbb-135">Recuperação de entrada arriscada</span><span class="sxs-lookup"><span data-stu-id="b1bbb-135">Risky sign-in recovery</span></span>
<span data-ttu-id="b1bbb-136">Quando um administrador tiver configurado uma política para entrar riscos, Olá afetado serão notificados quando eles tentam toosign-in.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-136">When an administrator has configured a policy for sign-in risks, hello affected users are notified when they try toosign-in.</span></span> 

<span data-ttu-id="b1bbb-137">**fluxo de entrada arriscados Olá tem duas etapas:**</span><span class="sxs-lookup"><span data-stu-id="b1bbb-137">**hello risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="b1bbb-138">usuário de saudação é informado de que algo incomum foi detectado sobre sua entrada no sistema, como fazendo logon em um novo local, dispositivo ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-138">hello user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="b1bbb-139">![Correção](./media/active-directory-identityprotection-flows/120.png "Correção")</span><span class="sxs-lookup"><span data-stu-id="b1bbb-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="b1bbb-140">usuário Olá é necessário tooprove sua identidade, resolvendo um desafio de segurança.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-140">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="b1bbb-141">Se o usuário hello está registrado para autenticação multifator precisam tooround-viagem e um número de telefone de tootheir de código de segurança.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-141">If hello user is registered for multi-factor authentication they need tooround-trip a security code tootheir phone number.</span></span> <span data-ttu-id="b1bbb-142">Como esta é apenas uma entrada arriscada e não uma conta comprometida, usuário Olá não tenha senha de saudação toochange neste fluxo.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-142">Since this is a just a risky sign in and not a compromised account, hello user won’t have toochange hello password in this flow.</span></span> 
   
    <span data-ttu-id="b1bbb-143">![Correção](./media/active-directory-identityprotection-flows/121.png "Correção")</span><span class="sxs-lookup"><span data-stu-id="b1bbb-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="b1bbb-144">Entrada arriscada bloqueada</span><span class="sxs-lookup"><span data-stu-id="b1bbb-144">Risky sign-in blocked</span></span>
<span data-ttu-id="b1bbb-145">Os administradores também podem optar tooset entrar risco política tooblock aos usuários após entrar dependendo do nível de risco de saudação.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-145">Administrators can also choose tooset a Sign-In Risk policy tooblock users upon sign-in depending on hello risk level.</span></span> <span data-ttu-id="b1bbb-146">tooget desbloqueado, os usuários finais devem entrar em contato com um administrador ou suporte técnico ou tente entrando de um dispositivo ou local familiar.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-146">tooget unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="b1bbb-147">Não é possível recuperar-se sozinho com uma solução de autenticação multifator neste caso.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="b1bbb-148">![Correção](./media/active-directory-identityprotection-flows/200.png "Correção")</span><span class="sxs-lookup"><span data-stu-id="b1bbb-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="b1bbb-149">Recuperação de conta comprometida</span><span class="sxs-lookup"><span data-stu-id="b1bbb-149">Compromised account recovery</span></span>
<span data-ttu-id="b1bbb-150">Quando uma política de segurança de risco do usuário tiver sido configurada, os usuários que atendem usuário Olá corre o risco de nível especificado na política de saudação (e, portanto, serão considerados comprometidos) deve passar pelo fluxo de recuperação de comprometimento de usuário Olá antes que eles podem entrar.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-150">When a user risk security policy has been configured, users who meet hello user risk level specified in hello policy (and are therefore assumed compromised) must go through hello user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="b1bbb-151">**fluxo de recuperação de comprometimento de usuário Olá tem três etapas:**</span><span class="sxs-lookup"><span data-stu-id="b1bbb-151">**hello user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="b1bbb-152">usuário de saudação é informado de que a segurança da conta está em risco devido a atividades suspeitas ou vazadas credenciais.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-152">hello user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="b1bbb-153">![Correção](./media/active-directory-identityprotection-flows/101.png "Correção")</span><span class="sxs-lookup"><span data-stu-id="b1bbb-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="b1bbb-154">usuário Olá é necessário tooprove sua identidade, resolvendo um desafio de segurança.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-154">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="b1bbb-155">Se o usuário hello está registrado para autenticação multifator, eles podem recuperar automaticamente sejam comprometidos.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-155">If hello user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="b1bbb-156">Será necessário tooround-viagem e um número de telefone de tootheir de código de segurança.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-156">They will need tooround-trip a security code tootheir phone number.</span></span> 
   
   <span data-ttu-id="b1bbb-157">![Correção](./media/active-directory-identityprotection-flows/110.png "Correção")</span><span class="sxs-lookup"><span data-stu-id="b1bbb-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="b1bbb-158">Olá, finalmente, o usuário é forçado toochange sua senha porque outra pessoa pode ter tido acesso tootheir conta.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-158">Finally, hello user is forced toochange their password since someone else may have had access tootheir account.</span></span> 
   <span data-ttu-id="b1bbb-159">Veja as capturas de tela desta experiência abaixo.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="b1bbb-160">![Correção](./media/active-directory-identityprotection-flows/111.png "Correção")</span><span class="sxs-lookup"><span data-stu-id="b1bbb-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="b1bbb-161">Conta comprometida bloqueada</span><span class="sxs-lookup"><span data-stu-id="b1bbb-161">Compromised account blocked</span></span>
<span data-ttu-id="b1bbb-162">tooget um usuário que foi bloqueado por uma política de segurança do usuário risco desbloqueada, o usuário Olá deve contatar um administrador ou o suporte técnico.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-162">tooget a user that was blocked by a user risk security policy unblocked, hello user must contact an administrator or help desk.</span></span> <span data-ttu-id="b1bbb-163">Não é possível recuperar-se sozinho com uma solução de autenticação multifator neste caso.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="b1bbb-164">![Correção](./media/active-directory-identityprotection-flows/104.png "Correção")</span><span class="sxs-lookup"><span data-stu-id="b1bbb-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="b1bbb-165">Redefinir senha</span><span class="sxs-lookup"><span data-stu-id="b1bbb-165">Reset password</span></span>
<span data-ttu-id="b1bbb-166">Caso os usuários comprometidos sejam impedidos de entrar, um administrador poderá gerar uma senha temporária para eles.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="b1bbb-167">Olá usuários terão toochange sua senha durante uma próxima vez que entrar.</span><span class="sxs-lookup"><span data-stu-id="b1bbb-167">hello users will have toochange their password during a next sign-in.</span></span>

<span data-ttu-id="b1bbb-168">![Correção](./media/active-directory-identityprotection-flows/160.png "Correção")</span><span class="sxs-lookup"><span data-stu-id="b1bbb-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="b1bbb-169">Consulte também</span><span class="sxs-lookup"><span data-stu-id="b1bbb-169">See also</span></span>
* [<span data-ttu-id="b1bbb-170">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="b1bbb-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

