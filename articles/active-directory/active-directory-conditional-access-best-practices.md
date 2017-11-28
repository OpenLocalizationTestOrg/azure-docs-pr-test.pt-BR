---
title: "práticas recomendadas de aaaBest para acesso condicional no Active Directory do Azure | Microsoft Docs"
description: "Saiba sobre o que você deve saber e o que você deve evitar fazer ao configurar políticas de acesso condicional."
services: active-directory
keywords: "tooapps de acesso condicional, o acesso condicional com o AD do Azure, proteger o acesso toocompany recursos, políticas de acesso condicional"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="3abc7-104">Práticas recomendadas para o acesso condicional no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3abc7-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="3abc7-105">Este tópico fornece informações sobre o que você deve saber e o que você deve evitar fazer ao configurar políticas de acesso condicional.</span><span class="sxs-lookup"><span data-stu-id="3abc7-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="3abc7-106">Antes de ler este tópico, você deve se familiarizar com os conceitos de saudação e terminologia Olá descritas em [acesso condicional no Active Directory do Azure](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3abc7-106">Before reading this topic, you should familiarize yourself with hello concepts and hello terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="3abc7-107">O que você deve saber</span><span class="sxs-lookup"><span data-stu-id="3abc7-107">What you should know</span></span>

### <a name="whats-required-toomake-a-policy-work"></a><span data-ttu-id="3abc7-108">O que é necessário um trabalho de política de toomake?</span><span class="sxs-lookup"><span data-stu-id="3abc7-108">What’s required toomake a policy work?</span></span>

<span data-ttu-id="3abc7-109">Quando você cria uma nova política, não há nenhum usuário, grupo, aplicativo ou controle de acesso selecionado.</span><span class="sxs-lookup"><span data-stu-id="3abc7-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![Aplicativos na nuvem](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="3abc7-111">toomake sua política de trabalho, você deve configurar a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="3abc7-111">toomake your policy work, you must configure hello following:</span></span>


|<span data-ttu-id="3abc7-112">O que</span><span class="sxs-lookup"><span data-stu-id="3abc7-112">What</span></span>           | <span data-ttu-id="3abc7-113">Como</span><span class="sxs-lookup"><span data-stu-id="3abc7-113">How</span></span>                                  | <span data-ttu-id="3abc7-114">Porque</span><span class="sxs-lookup"><span data-stu-id="3abc7-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="3abc7-115">**Aplicativos na nuvem**</span><span class="sxs-lookup"><span data-stu-id="3abc7-115">**Cloud apps**</span></span> |<span data-ttu-id="3abc7-116">Você precisa de um ou mais aplicativos tooselect.</span><span class="sxs-lookup"><span data-stu-id="3abc7-116">You need tooselect one or more apps.</span></span>  | <span data-ttu-id="3abc7-117">meta de saudação de uma política de acesso condicional é tooenable toofine ajustar como os usuários autorizados podem acessar seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3abc7-117">hello goal of a conditional access policy is tooenable you toofine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="3abc7-118">**Usuários e grupos**</span><span class="sxs-lookup"><span data-stu-id="3abc7-118">**Users and groups**</span></span> | <span data-ttu-id="3abc7-119">Você precisa tooselect pelo menos um usuário ou grupo que é autorizado tooaccess Olá aplicativos na nuvem selecionada.</span><span class="sxs-lookup"><span data-stu-id="3abc7-119">You need tooselect at least one user or group that is authorized tooaccess hello cloud apps you have selected.</span></span> | <span data-ttu-id="3abc7-120">Uma política de acesso condicional que não tenha usuários e grupos atribuídos nunca será disparada.</span><span class="sxs-lookup"><span data-stu-id="3abc7-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="3abc7-121">**Controles de acesso**</span><span class="sxs-lookup"><span data-stu-id="3abc7-121">**Access controls**</span></span> | <span data-ttu-id="3abc7-122">Você precisa tooselect pelo menos um controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="3abc7-122">You need tooselect at least one access control.</span></span> | <span data-ttu-id="3abc7-123">O processador de diretiva precisa tooknow que toodo se as condições forem atendidas.</span><span class="sxs-lookup"><span data-stu-id="3abc7-123">Your policy processor needs tooknow what toodo if your conditions are satisfied.</span></span>|


<span data-ttu-id="3abc7-124">Requisitos básicos de adição toothese, em muitos casos, você também deve configurar uma condição.</span><span class="sxs-lookup"><span data-stu-id="3abc7-124">In addition toothese basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="3abc7-125">Enquanto uma política também funcionaria sem uma condição configurada, as condições são um fator importante Olá para ajustar o acesso tooyour aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3abc7-125">While a policy would also work without a configured condition, conditions are hello driving factor for fine-tuning access tooyour apps.</span></span>


![Aplicativos na nuvem](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="3abc7-127">Como as atribuições são avaliadas?</span><span class="sxs-lookup"><span data-stu-id="3abc7-127">How are assignments evaluated?</span></span>

<span data-ttu-id="3abc7-128">Todas as atribuições são avaliadas com **AND** lógicos.</span><span class="sxs-lookup"><span data-stu-id="3abc7-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="3abc7-129">Se você tiver mais de uma atribuição configurada, tootrigger uma política, todas as atribuições devem ser atendidas.</span><span class="sxs-lookup"><span data-stu-id="3abc7-129">If you have more than one assignment configured, tootrigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="3abc7-130">Se você precisar tooconfigure uma condição de local que se aplica a conexões tooall provenientes de fora da rede da sua organização, você pode fazer isso por:</span><span class="sxs-lookup"><span data-stu-id="3abc7-130">If you need tooconfigure a location condition that applies tooall connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="3abc7-131">Incluindo **todos os locais**</span><span class="sxs-lookup"><span data-stu-id="3abc7-131">Including **All locations**</span></span>
- <span data-ttu-id="3abc7-132">Excluindo **todos os IPs confiáveis**</span><span class="sxs-lookup"><span data-stu-id="3abc7-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="3abc7-133">O que acontece se você tiver políticas no hello portal clássico do Azure e o portal do Azure configurado?</span><span class="sxs-lookup"><span data-stu-id="3abc7-133">What happens if you have policies in hello Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="3abc7-134">Ambas as políticas são aplicadas pelo Active Directory do Azure e o usuário Olá obtém acesso somente quando todos os requisitos são atendidos.</span><span class="sxs-lookup"><span data-stu-id="3abc7-134">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a><span data-ttu-id="3abc7-135">O que acontece se você tiver políticas no hello portal Intune Silverlight e hello Portal do Azure?</span><span class="sxs-lookup"><span data-stu-id="3abc7-135">What happens if you have policies in hello Intune Silverlight portal and hello Azure Portal?</span></span>
<span data-ttu-id="3abc7-136">Ambas as políticas são aplicadas pelo Active Directory do Azure e o usuário Olá obtém acesso somente quando todos os requisitos são atendidos.</span><span class="sxs-lookup"><span data-stu-id="3abc7-136">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a><span data-ttu-id="3abc7-137">O que acontece se eu tiver várias políticas para Olá configurado pelo mesmo usuário?</span><span class="sxs-lookup"><span data-stu-id="3abc7-137">What happens if I have multiple policies for hello same user configured?</span></span>  
<span data-ttu-id="3abc7-138">Para cada entrada, o Azure Active Directory avalia todas as políticas e garante que todos os requisitos são atendidos antes de usuário de toohello acesso concedido.</span><span class="sxs-lookup"><span data-stu-id="3abc7-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access toohello user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="3abc7-139">O acesso condicional funciona com o Exchange ActiveSync?</span><span class="sxs-lookup"><span data-stu-id="3abc7-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="3abc7-140">Sim, você não pode usar o Exchange ActiveSync em uma política de acesso condicional.</span><span class="sxs-lookup"><span data-stu-id="3abc7-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="3abc7-141">O que você deve evitar</span><span class="sxs-lookup"><span data-stu-id="3abc7-141">What you should avoid doing</span></span>

<span data-ttu-id="3abc7-142">estrutura de acesso condicional Olá fornece uma excelente flexibilidade.</span><span class="sxs-lookup"><span data-stu-id="3abc7-142">hello conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="3abc7-143">No entanto, grande flexibilidade também significa que você deve rever cuidadosamente cada tooreleasing anterior de política de configuração-resultados indesejáveis tooavoid.</span><span class="sxs-lookup"><span data-stu-id="3abc7-143">However, great flexibility  also means that you should carefully review each configuration policy prior tooreleasing it tooavoid undesirable results.</span></span> <span data-ttu-id="3abc7-144">Nesse contexto, você deve prestar atenção especial tooassignments afetar conjuntos como **todos os usuários / grupos / aplicativos de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="3abc7-144">In this context, you should pay special attention tooassignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="3abc7-145">Em seu ambiente, você deve evitar Olá configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="3abc7-145">In your environment, you should avoid hello following configurations:</span></span>


<span data-ttu-id="3abc7-146">**Para todos os usuários, todos os aplicativos de nuvem:**</span><span class="sxs-lookup"><span data-stu-id="3abc7-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="3abc7-147">**Bloquear o acesso** - Essa configuração bloqueia toda a organização, o que certamente não é uma boa ideia.</span><span class="sxs-lookup"><span data-stu-id="3abc7-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="3abc7-148">**Requer dispositivo compatível** - para usuários que não tiverem registrado seus dispositivos ao mesmo tempo, essa política bloqueia o acesso de todos os incluindo acesso toohello Intune portal.</span><span class="sxs-lookup"><span data-stu-id="3abc7-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access toohello Intune portal.</span></span> <span data-ttu-id="3abc7-149">Se você for um administrador sem um dispositivo registrado, esta política impede que você voltar para a diretiva de Olá Olá toochange portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3abc7-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into hello Azure portal toochange hello policy.</span></span>

- <span data-ttu-id="3abc7-150">**Exigir o ingresso no domínio** - este bloco de diretiva acesso tem também Olá potencial tooblock acesso para todos os usuários em sua organização se você ainda não tiver um dispositivo ingressado no domínio.</span><span class="sxs-lookup"><span data-stu-id="3abc7-150">**Require domain join** - This policy block access has also hello potential tooblock access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="3abc7-151">**Para todos os usuários, todos os aplicativos de nuvem, todas as plataformas de dispositivo:**</span><span class="sxs-lookup"><span data-stu-id="3abc7-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="3abc7-152">**Bloquear o acesso** - Essa configuração bloqueia toda a organização, o que certamente não é uma boa ideia.</span><span class="sxs-lookup"><span data-stu-id="3abc7-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="3abc7-153">Cenários comuns</span><span class="sxs-lookup"><span data-stu-id="3abc7-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="3abc7-154">Exibir a autenticação multifator para aplicativos</span><span class="sxs-lookup"><span data-stu-id="3abc7-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="3abc7-155">Muitos ambientes têm aplicativos que exigem um nível mais alto de proteção que Olá outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="3abc7-155">Many environments have apps requiring a higher level of protection than hello others.</span></span>
<span data-ttu-id="3abc7-156">Isso acontece, por exemplo, Olá para aplicativos que têm acesso toosensitive dados.</span><span class="sxs-lookup"><span data-stu-id="3abc7-156">This is, for example, hello case for apps that have access toosensitive data.</span></span>
<span data-ttu-id="3abc7-157">Se você quiser tooadd outra camada de proteção toothese aplicativos, você pode configurar uma política de acesso condicional que requer autenticação multifator quando os usuários acessam esses aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3abc7-157">If you want tooadd another layer of protection toothese apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="3abc7-158">Exigir autenticação multifator para acesso de redes que não são confiáveis</span><span class="sxs-lookup"><span data-stu-id="3abc7-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="3abc7-159">Esse cenário é semelhante cenário anterior de toohello porque ele adiciona um requisito para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="3abc7-159">This scenario is similar toohello previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="3abc7-160">No entanto, Olá principal diferença é a condição Olá para este requisito.</span><span class="sxs-lookup"><span data-stu-id="3abc7-160">However, hello main difference is hello condition for this requirement.</span></span>  
<span data-ttu-id="3abc7-161">Enquanto o foco de saudação do cenário anterior Olá estava em aplicativos com dados do access toosensitve, Olá foco deste cenário é locais confiáveis.</span><span class="sxs-lookup"><span data-stu-id="3abc7-161">While hello focus of hello previous scenario was on apps with access toosensitve data, hello focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="3abc7-162">Em outras palavras, você pode ter um requisito para autenticação multifator se um aplicativo for acessado por um usuário de uma rede em que você não confia.</span><span class="sxs-lookup"><span data-stu-id="3abc7-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="3abc7-163">Somente os dispositivos confiáveis podem acessar os serviços do Office 365</span><span class="sxs-lookup"><span data-stu-id="3abc7-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="3abc7-164">Se você estiver usando o Intune em seu ambiente, você pode começar imediatamente usando a interface de política de acesso condicional Olá na Olá console do Azure.</span><span class="sxs-lookup"><span data-stu-id="3abc7-164">If you are using Intune in your environment, you can immediately start using hello conditional access policy interface in hello Azure console.</span></span>

<span data-ttu-id="3abc7-165">Muitos clientes do Intune estão usando tooensure de acesso condicional que somente dispositivos confiáveis podem acessar os serviços do Office 365.</span><span class="sxs-lookup"><span data-stu-id="3abc7-165">Many Intune customers are using conditional access tooensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="3abc7-166">Isso significa que os dispositivos móveis registrados com o Intune e atender aos requisitos da política de conformidade e PCs com Windows são tooan ingressado no domínio de local.</span><span class="sxs-lookup"><span data-stu-id="3abc7-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined tooan on-premises domain.</span></span> <span data-ttu-id="3abc7-167">Das principais melhorias é que você não tem tooset hello mesma política para cada um dos serviços de saudação Office 365.</span><span class="sxs-lookup"><span data-stu-id="3abc7-167">A key improvement is that you do not have tooset hello same policy for each of hello Office 365 services.</span></span>  <span data-ttu-id="3abc7-168">Quando você cria uma nova política, configure Olá nuvem aplicativos tooinclude cada de saudação O365 aplicativos que você deseja tooprotect com acesso condicional.</span><span class="sxs-lookup"><span data-stu-id="3abc7-168">When you create a new policy, configure hello Cloud apps tooinclude each of hello O365 apps that you wish tooprotect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3abc7-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3abc7-169">Next steps</span></span>

<span data-ttu-id="3abc7-170">Se você quiser tooknow como tooconfigure uma política de acesso condicional, consulte [Introdução ao acesso condicional no Active Directory do Azure](active-directory-conditional-access-azure-portal-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3abc7-170">If you want tooknow how tooconfigure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
