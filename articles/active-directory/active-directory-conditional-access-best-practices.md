---
title: "Práticas recomendadas para o acesso condicional no Azure Active Directory | Microsoft Docs"
description: "Saiba sobre o que você deve saber e o que você deve evitar fazer ao configurar políticas de acesso condicional."
services: active-directory
keywords: "acesso condicional para aplicativos, acesso condicional com o Azure AD, acesso seguro aos recursos da empresa, políticas de acesso condicional"
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
ms.openlocfilehash: 3e524c116479c1af6eb6a601c9b57d27a697c5a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="5a707-104">Práticas recomendadas para o acesso condicional no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5a707-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="5a707-105">Este tópico fornece informações sobre o que você deve saber e o que você deve evitar fazer ao configurar políticas de acesso condicional.</span><span class="sxs-lookup"><span data-stu-id="5a707-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="5a707-106">Antes de ler este tópico, você deve se familiarizar com os conceitos e a terminologia descritos em [Acesso condicional no Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5a707-106">Before reading this topic, you should familiarize yourself with the concepts and the terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="5a707-107">O que você deve saber</span><span class="sxs-lookup"><span data-stu-id="5a707-107">What you should know</span></span>

### <a name="whats-required-to-make-a-policy-work"></a><span data-ttu-id="5a707-108">O que é necessário para fazer uma política funcionar?</span><span class="sxs-lookup"><span data-stu-id="5a707-108">What’s required to make a policy work?</span></span>

<span data-ttu-id="5a707-109">Quando você cria uma nova política, não há nenhum usuário, grupo, aplicativo ou controle de acesso selecionado.</span><span class="sxs-lookup"><span data-stu-id="5a707-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![Aplicativos na nuvem](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="5a707-111">Para fazer sua política funcionar, você deve configurar o seguinte:</span><span class="sxs-lookup"><span data-stu-id="5a707-111">To make your policy work, you must configure the following:</span></span>


|<span data-ttu-id="5a707-112">O que</span><span class="sxs-lookup"><span data-stu-id="5a707-112">What</span></span>           | <span data-ttu-id="5a707-113">Como</span><span class="sxs-lookup"><span data-stu-id="5a707-113">How</span></span>                                  | <span data-ttu-id="5a707-114">Porque</span><span class="sxs-lookup"><span data-stu-id="5a707-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="5a707-115">**Aplicativos na nuvem**</span><span class="sxs-lookup"><span data-stu-id="5a707-115">**Cloud apps**</span></span> |<span data-ttu-id="5a707-116">Você precisa selecionar um ou mais aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5a707-116">You need to select one or more apps.</span></span>  | <span data-ttu-id="5a707-117">A meta de uma política de acesso condicional é habilitar você a ajustar como os usuários autorizados podem acessar seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5a707-117">The goal of a conditional access policy is to enable you to fine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="5a707-118">**Usuários e grupos**</span><span class="sxs-lookup"><span data-stu-id="5a707-118">**Users and groups**</span></span> | <span data-ttu-id="5a707-119">Você precisa selecionar pelo menos um usuário ou grupo autorizado a acessar os aplicativos na nuvem que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="5a707-119">You need to select at least one user or group that is authorized to access the cloud apps you have selected.</span></span> | <span data-ttu-id="5a707-120">Uma política de acesso condicional que não tenha usuários e grupos atribuídos nunca será disparada.</span><span class="sxs-lookup"><span data-stu-id="5a707-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="5a707-121">**Controles de acesso**</span><span class="sxs-lookup"><span data-stu-id="5a707-121">**Access controls**</span></span> | <span data-ttu-id="5a707-122">Você precisa selecionar pelo menos um controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="5a707-122">You need to select at least one access control.</span></span> | <span data-ttu-id="5a707-123">O processador de políticas precisa saber o que fazer se as condições forem atendidas.</span><span class="sxs-lookup"><span data-stu-id="5a707-123">Your policy processor needs to know what to do if your conditions are satisfied.</span></span>|


<span data-ttu-id="5a707-124">Além desses requisitos básicos, em muitos casos, você também precisa configurar uma condição.</span><span class="sxs-lookup"><span data-stu-id="5a707-124">In addition to these basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="5a707-125">Enquanto uma política também funcione sem uma condição configurada, as condições são o fator determinante para ajustar o acesso aos seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5a707-125">While a policy would also work without a configured condition, conditions are the driving factor for fine-tuning access to your apps.</span></span>


![Aplicativos na nuvem](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="5a707-127">Como as atribuições são avaliadas?</span><span class="sxs-lookup"><span data-stu-id="5a707-127">How are assignments evaluated?</span></span>

<span data-ttu-id="5a707-128">Todas as atribuições são avaliadas com **AND** lógicos.</span><span class="sxs-lookup"><span data-stu-id="5a707-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="5a707-129">Se você tiver mais de uma atribuição configurada, para disparar uma política, todas as atribuições deverão ser satisfeitas.</span><span class="sxs-lookup"><span data-stu-id="5a707-129">If you have more than one assignment configured, to trigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="5a707-130">Se você precisar configurar uma condição de local que se aplique a todas as conexões feitas de fora da rede da sua organização, poderá fazer isso:</span><span class="sxs-lookup"><span data-stu-id="5a707-130">If you need to configure a location condition that applies to all connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="5a707-131">Incluindo **todos os locais**</span><span class="sxs-lookup"><span data-stu-id="5a707-131">Including **All locations**</span></span>
- <span data-ttu-id="5a707-132">Excluindo **todos os IPs confiáveis**</span><span class="sxs-lookup"><span data-stu-id="5a707-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-the-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="5a707-133">O que acontece se você tiver políticas configuradas no portal clássico do Azure e no portal do Azure?</span><span class="sxs-lookup"><span data-stu-id="5a707-133">What happens if you have policies in the Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="5a707-134">Ambas as políticas são aplicadas pelo Azure Active Directory e o usuário só obterá acesso quando todos os requisitos forem atendidos.</span><span class="sxs-lookup"><span data-stu-id="5a707-134">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-the-intune-silverlight-portal-and-the-azure-portal"></a><span data-ttu-id="5a707-135">O que acontece se você tiver políticas no portal do Intune Silverlight e no Portal do Azure?</span><span class="sxs-lookup"><span data-stu-id="5a707-135">What happens if you have policies in the Intune Silverlight portal and the Azure Portal?</span></span>
<span data-ttu-id="5a707-136">Ambas as políticas são aplicadas pelo Azure Active Directory e o usuário só obterá acesso quando todos os requisitos forem atendidos.</span><span class="sxs-lookup"><span data-stu-id="5a707-136">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-the-same-user-configured"></a><span data-ttu-id="5a707-137">O que acontece se eu tiver várias políticas configuradas para o mesmo usuário?</span><span class="sxs-lookup"><span data-stu-id="5a707-137">What happens if I have multiple policies for the same user configured?</span></span>  
<span data-ttu-id="5a707-138">Para cada entrada, o Azure Active Directory avalia todas as políticas e garante que todos os requisitos sejam atendidos antes que o acesso seja concedido ao usuário.</span><span class="sxs-lookup"><span data-stu-id="5a707-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access to the user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="5a707-139">O acesso condicional funciona com o Exchange ActiveSync?</span><span class="sxs-lookup"><span data-stu-id="5a707-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="5a707-140">Sim, você não pode usar o Exchange ActiveSync em uma política de acesso condicional.</span><span class="sxs-lookup"><span data-stu-id="5a707-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="5a707-141">O que você deve evitar</span><span class="sxs-lookup"><span data-stu-id="5a707-141">What you should avoid doing</span></span>

<span data-ttu-id="5a707-142">A estrutura de acesso condicional fornece uma excelente flexibilidade de configuração.</span><span class="sxs-lookup"><span data-stu-id="5a707-142">The conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="5a707-143">No entanto, muita flexibilidade também significa que você deve examinar cuidadosamente cada política de configuração antes de liberá-la, a fim de evitar resultados indesejados.</span><span class="sxs-lookup"><span data-stu-id="5a707-143">However, great flexibility  also means that you should carefully review each configuration policy prior to releasing it to avoid undesirable results.</span></span> <span data-ttu-id="5a707-144">Nesse contexto, preste atenção especial às atribuições que afetam conjuntos completos, como **todos os usuários/grupos/aplicativos de nuvem**.</span><span class="sxs-lookup"><span data-stu-id="5a707-144">In this context, you should pay special attention to assignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="5a707-145">Em seu ambiente, evite as configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a707-145">In your environment, you should avoid the following configurations:</span></span>


<span data-ttu-id="5a707-146">**Para todos os usuários, todos os aplicativos de nuvem:**</span><span class="sxs-lookup"><span data-stu-id="5a707-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="5a707-147">**Bloquear o acesso** - Essa configuração bloqueia toda a organização, o que certamente não é uma boa ideia.</span><span class="sxs-lookup"><span data-stu-id="5a707-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="5a707-148">**Exigir dispositivo compatível** - Para usuários que ainda não registraram seus dispositivos, esta política bloqueia todo acesso, incluindo acesso ao portal do Intune.</span><span class="sxs-lookup"><span data-stu-id="5a707-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access to the Intune portal.</span></span> <span data-ttu-id="5a707-149">Se você for um administrador sem um dispositivo registrado, essa política impedirá você voltar ao Portal do Azure para alterar a política.</span><span class="sxs-lookup"><span data-stu-id="5a707-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into the Azure portal to change the policy.</span></span>

- <span data-ttu-id="5a707-150">**Exigir ingresso no domínio** - Esta política de bloqueio de acesso também tem o potencial para bloquear o acesso de todos os usuários em sua organização se você ainda não tiver um dispositivo ingressado no domínio.</span><span class="sxs-lookup"><span data-stu-id="5a707-150">**Require domain join** - This policy block access has also the potential to block access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="5a707-151">**Para todos os usuários, todos os aplicativos de nuvem, todas as plataformas de dispositivo:**</span><span class="sxs-lookup"><span data-stu-id="5a707-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="5a707-152">**Bloquear o acesso** - Essa configuração bloqueia toda a organização, o que certamente não é uma boa ideia.</span><span class="sxs-lookup"><span data-stu-id="5a707-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="5a707-153">Cenários comuns</span><span class="sxs-lookup"><span data-stu-id="5a707-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="5a707-154">Exibir a autenticação multifator para aplicativos</span><span class="sxs-lookup"><span data-stu-id="5a707-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="5a707-155">Muitos ambientes têm aplicativos que exigem um nível mais alto de proteção do que outros.</span><span class="sxs-lookup"><span data-stu-id="5a707-155">Many environments have apps requiring a higher level of protection than the others.</span></span>
<span data-ttu-id="5a707-156">Isso é, por exemplo, o caso para aplicativos que têm acesso a dados confidenciais.</span><span class="sxs-lookup"><span data-stu-id="5a707-156">This is, for example, the case for apps that have access to sensitive data.</span></span>
<span data-ttu-id="5a707-157">Se você quiser adicionar outra camada de proteção para esses aplicativos, poderá configurar uma política de acesso condicional que exija a autenticação multifator quando os usuários acessarem esses aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5a707-157">If you want to add another layer of protection to these apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="5a707-158">Exigir autenticação multifator para acesso de redes que não são confiáveis</span><span class="sxs-lookup"><span data-stu-id="5a707-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="5a707-159">Esse cenário é semelhante ao cenário anterior porque adiciona um requisito para a autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="5a707-159">This scenario is similar to the previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="5a707-160">No entanto, a principal diferença é a condição para esse requisito.</span><span class="sxs-lookup"><span data-stu-id="5a707-160">However, the main difference is the condition for this requirement.</span></span>  
<span data-ttu-id="5a707-161">Embora o foco do cenário anterior fosse aplicativos com acesso a dados confidenciais, o foco deste cenário é em locais confiáveis.</span><span class="sxs-lookup"><span data-stu-id="5a707-161">While the focus of the previous scenario was on apps with access to sensitve data, the focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="5a707-162">Em outras palavras, você pode ter um requisito para autenticação multifator se um aplicativo for acessado por um usuário de uma rede em que você não confia.</span><span class="sxs-lookup"><span data-stu-id="5a707-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="5a707-163">Somente os dispositivos confiáveis podem acessar os serviços do Office 365</span><span class="sxs-lookup"><span data-stu-id="5a707-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="5a707-164">Se você estiver usando o Intune em seu ambiente, poderá começar imediatamente usando a interface de política de acesso condicional no console do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a707-164">If you are using Intune in your environment, you can immediately start using the conditional access policy interface in the Azure console.</span></span>

<span data-ttu-id="5a707-165">Muitos clientes do Intune estão usando o acesso condicional para garantir que somente os dispositivos confiáveis possam acessar os serviços do Office 365.</span><span class="sxs-lookup"><span data-stu-id="5a707-165">Many Intune customers are using conditional access to ensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="5a707-166">Isso significa que os dispositivos móveis estão registrados no Intune e atendem aos requisitos da política de conformidade e que os computadores com Windows fazem parte de um domínio local.</span><span class="sxs-lookup"><span data-stu-id="5a707-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined to an on-premises domain.</span></span> <span data-ttu-id="5a707-167">Uma melhoria-chave é que você não precisa definir a mesma política para cada um dos serviços do Office 365.</span><span class="sxs-lookup"><span data-stu-id="5a707-167">A key improvement is that you do not have to set the same policy for each of the Office 365 services.</span></span>  <span data-ttu-id="5a707-168">Quando você criar uma nova política, configure os aplicativos de nuvem para incluir cada um dos aplicativos do O365 que você deseja proteger com o acesso condicional.</span><span class="sxs-lookup"><span data-stu-id="5a707-168">When you create a new policy, configure the Cloud apps to include each of the O365 apps that you wish to protect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a707-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a707-169">Next steps</span></span>

<span data-ttu-id="5a707-170">Se você quiser saber como configurar uma política de acesso condicional, veja [Introdução ao acesso condicional no Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5a707-170">If you want to know how to configure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
