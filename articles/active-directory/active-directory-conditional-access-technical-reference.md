---
title: "Referência técnica do acesso condicional ao Azure Active Directory | Microsoft Docs"
description: "Com o controle de acesso condicional, o Active Directory do Azure verifica as condições específicas escolhidas para autenticação do usuário, antes de permitir o acesso ao aplicativo. Quando essas condições forem atendidas, o usuário é autenticado e autorizado a acessar o aplicativo."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ca16a5399f94fd1ab267e0798cade3fd83f75b13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="5bb94-104">Referência técnica do acesso condicional ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5bb94-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="5bb94-105">Serviços habilitados com acesso condicional</span><span class="sxs-lookup"><span data-stu-id="5bb94-105">Services enabled with conditional access</span></span>

<span data-ttu-id="5bb94-106">Regras de acesso condicional têm suporte em vários tipos de aplicativos do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bb94-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="5bb94-107">Essa lista inclui:</span><span class="sxs-lookup"><span data-stu-id="5bb94-107">This list includes:</span></span>


* <span data-ttu-id="5bb94-108">Aplicativos registrados com o Proxy de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="5bb94-108">Applications registered with the Azure Application Proxy</span></span>
* <span data-ttu-id="5bb94-109">Aplicativo Remoto do Azure</span><span class="sxs-lookup"><span data-stu-id="5bb94-109">Azure Remote App</span></span>
* <span data-ttu-id="5bb94-110">Aplicativos de linha de negócios e de multilocação desenvolvidos registrados no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5bb94-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="5bb94-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="5bb94-111">Dynamics CRM</span></span>
* <span data-ttu-id="5bb94-112">Aplicativos federados da galeria de aplicativos do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bb94-112">Federated applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="5bb94-113">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="5bb94-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="5bb94-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="5bb94-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="5bb94-115">Microsoft Office 365 SharePoint Online (inclui o OneDrive for Business)</span><span class="sxs-lookup"><span data-stu-id="5bb94-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="5bb94-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="5bb94-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="5bb94-117">Aplicativos de SSO de senha da galeria de aplicativos do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bb94-117">Password SSO applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="5bb94-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="5bb94-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="5bb94-119">Equipes da Microsoft</span><span class="sxs-lookup"><span data-stu-id="5bb94-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="5bb94-120">Habilitar regras de acesso</span><span class="sxs-lookup"><span data-stu-id="5bb94-120">Enable access rules</span></span>
<span data-ttu-id="5bb94-121">Cada regra pode ser habilitada ou desabilitada com base no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bb94-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="5bb94-122">Quando as regras estão **ATIVADAS** , elas são habilitadas e impostas aos usuários que acessam o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bb94-122">When rules are **ON** they will be enabled and enforced for users accessing the application.</span></span> <span data-ttu-id="5bb94-123">Quando estão **DESATIVADAS** , elas não são usadas e não afetam a experiência de entrada dos usuários.</span><span class="sxs-lookup"><span data-stu-id="5bb94-123">When they are **OFF** they will not be used and will not impact the users sign in experience.</span></span>

## <a name="applying-rules-to-specific-users"></a><span data-ttu-id="5bb94-124">Aplicar regras a usuários específicos</span><span class="sxs-lookup"><span data-stu-id="5bb94-124">Applying rules to specific users</span></span>
<span data-ttu-id="5bb94-125">As regras podem ser aplicadas a conjuntos específicos de usuários baseados no grupo de segurança definindo **Aplicar a**.</span><span class="sxs-lookup"><span data-stu-id="5bb94-125">Rules can be applied to specific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="5bb94-126">**Aplicar a** pode ser definido como **Todos os Usuários** ou **Grupos**.</span><span class="sxs-lookup"><span data-stu-id="5bb94-126">**Apply To** can be set to **All Users** or **Groups**.</span></span> <span data-ttu-id="5bb94-127">Quando definido como **Todos os Usuários** , as regras são aplicadas a qualquer usuário com acesso ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bb94-127">When set to **All Users** the rules will apply to any user with access to the application.</span></span> <span data-ttu-id="5bb94-128">A opção **Grupos** permite que grupos de segurança e de distribuição específicos sejam selecionados e as regras sejam impostas somente para esses grupos.</span><span class="sxs-lookup"><span data-stu-id="5bb94-128">The **Groups** option allows specific security and distribution groups to be selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="5bb94-129">Ao implantar uma regra, é comum aplicá-la primeiro a um conjunto limitado de usuários, que são membros de um grupo piloto.</span><span class="sxs-lookup"><span data-stu-id="5bb94-129">When deploying a rule,  it is common to first apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="5bb94-130">Após a conclusão, a regra pode ser aplicada a **Todos os Usuários**.</span><span class="sxs-lookup"><span data-stu-id="5bb94-130">Once complete the rule can be applied to **All Users**.</span></span> <span data-ttu-id="5bb94-131">Isso fará com que a regra a seja imposta a todos os usuários na organização.</span><span class="sxs-lookup"><span data-stu-id="5bb94-131">This will cause the rule to be enforced for all users in the organization.</span></span>

<span data-ttu-id="5bb94-132">Alguns grupos também podem ser isentos da política usando a opção **Exceto** .</span><span class="sxs-lookup"><span data-stu-id="5bb94-132">Select groups may also be exempted from policy using the **Except** option.</span></span> <span data-ttu-id="5bb94-133">Todos os membros desses grupos estarão isentos mesmo que apareçam em um grupo incluído.</span><span class="sxs-lookup"><span data-stu-id="5bb94-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="5bb94-134">Redes "No trabalho"</span><span class="sxs-lookup"><span data-stu-id="5bb94-134">“At work” networks</span></span>
<span data-ttu-id="5bb94-135">As regras de acesso condicional que usam uma rede "No trabalho" dependem de intervalos de endereços IP confiáveis que foram configurados no Azure AD ou que usam a declaração “inside corpnet” do AD FS.</span><span class="sxs-lookup"><span data-stu-id="5bb94-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of the "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="5bb94-136">Essas regras incluem:</span><span class="sxs-lookup"><span data-stu-id="5bb94-136">These rules include:</span></span>

* <span data-ttu-id="5bb94-137">Exigir autenticação multifator quando não está no trabalho</span><span class="sxs-lookup"><span data-stu-id="5bb94-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="5bb94-138">Bloquear acesso quando não estiver no trabalho</span><span class="sxs-lookup"><span data-stu-id="5bb94-138">Block access when not at work</span></span>

<span data-ttu-id="5bb94-139">Opções para especificar redes "no trabalho"</span><span class="sxs-lookup"><span data-stu-id="5bb94-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="5bb94-140">Configurar intervalos de endereços IP na [página de configurações da autenticação multifator](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="5bb94-140">Configure trusted IP address ranges in the [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="5bb94-141">A política de acesso condicional usará os intervalos configurados em cada solicitação de autenticação e emissão de token para avaliar as regras.</span><span class="sxs-lookup"><span data-stu-id="5bb94-141">Conditional Access policy will use the configured ranges on each authentication request and token issuance to evaluate rules.</span></span> 
2. <span data-ttu-id="5bb94-142">Configure o uso da declaração inside corpnet; essa opção pode ser usada com diretórios federados, usando o AD FS.</span><span class="sxs-lookup"><span data-stu-id="5bb94-142">Configure use of the inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="5bb94-143">Para saber mais sobre as declarações inside corpnet, veja [IPs confiáveis](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="5bb94-143">To learn more about the inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="5bb94-144">Regras com base na confidencialidade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="5bb94-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="5bb94-145">As regras são configuradas por aplicativo, permitindo que os serviços de alto valor sejam protegidos sem afetar o acesso a outros serviços.</span><span class="sxs-lookup"><span data-stu-id="5bb94-145">Rules are configured per application allowing the high value services to be secured without impacting access to other services.</span></span> <span data-ttu-id="5bb94-146">As regras de acesso condicional podem ser configuradas na guia **Configurar** do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bb94-146">Conditional access rules can be configured on the  **Configure** tab of the application.</span></span> 

<span data-ttu-id="5bb94-147">Regras oferecidas atualmente:</span><span class="sxs-lookup"><span data-stu-id="5bb94-147">Rules currently offered:</span></span>

* <span data-ttu-id="5bb94-148">**Exigir autenticação multifator**</span><span class="sxs-lookup"><span data-stu-id="5bb94-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="5bb94-149">Todos os usuários aos quais essa política se aplica deverão realizar a autenticação por meio da autenticação multifator pelo menos uma vez.</span><span class="sxs-lookup"><span data-stu-id="5bb94-149">All users that this policy is applied to will be required to authenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="5bb94-150">**Exigir autenticação multifator quando não está no trabalho**</span><span class="sxs-lookup"><span data-stu-id="5bb94-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="5bb94-151">Se essa política for aplicada, todos os usuários terão que ter realizado a autenticação multifator pelo menos uma vez se acessarem o serviço de um local remoto não comercial.</span><span class="sxs-lookup"><span data-stu-id="5bb94-151">If this policy is applied, all users will be required to have performed multi-factor authentication at least once if they access the service from a non-work remote location.</span></span> <span data-ttu-id="5bb94-152">Se os usuários saírem de um local de trabalho para um local remoto, precisarão realizar a autenticação multifator ao acessar o serviço.</span><span class="sxs-lookup"><span data-stu-id="5bb94-152">If they move from a work to remote location, they will be required to perform multifactor authentication when accessing the service.</span></span>
* <span data-ttu-id="5bb94-153">**Bloquear acesso quando não estiver no trabalho**</span><span class="sxs-lookup"><span data-stu-id="5bb94-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="5bb94-154">Quando os usuários saírem de um local de trabalho para um local remoto, eles serão bloqueados se a política “Bloquear acesso quando não estiver no trabalho” estiver aplicada a eles.</span><span class="sxs-lookup"><span data-stu-id="5bb94-154">When users move from work to a remote location, they will be blocked if the "Block access when not at work" policy is applied to them.</span></span>  <span data-ttu-id="5bb94-155">Eles terão o acesso permitido novamente quando estiverem em um local de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5bb94-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="5bb94-156">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="5bb94-156">Related topics</span></span>
* [<span data-ttu-id="5bb94-157">Proteger o acesso ao Office 365 e a outros aplicativos conectados ao Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5bb94-157">Securing access to Office 365 and other apps connected to Azure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="5bb94-158">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5bb94-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

