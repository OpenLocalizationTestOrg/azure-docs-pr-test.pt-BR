---
title: "Referência técnica do acesso condicional do Active Directory de aaaAzure | Microsoft Docs"
description: "Com controle de acesso condicional, o Active Directory do Azure verifica condições específicas hello, que você escolhe ao autenticar usuário hello e antes de permitir acesso toohello aplicativo. Quando essas condições forem atendidas, o usuário de Olá é autenticado e acesso toohello aplicativo autorizado."
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
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="ce82e-104">Referência técnica do acesso condicional ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce82e-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="ce82e-105">Serviços habilitados com acesso condicional</span><span class="sxs-lookup"><span data-stu-id="ce82e-105">Services enabled with conditional access</span></span>

<span data-ttu-id="ce82e-106">Regras de acesso condicional têm suporte em vários tipos de aplicativos do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce82e-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="ce82e-107">Essa lista inclui:</span><span class="sxs-lookup"><span data-stu-id="ce82e-107">This list includes:</span></span>


* <span data-ttu-id="ce82e-108">Aplicativos registrados com hello Proxy de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="ce82e-108">Applications registered with hello Azure Application Proxy</span></span>
* <span data-ttu-id="ce82e-109">Aplicativo Remoto do Azure</span><span class="sxs-lookup"><span data-stu-id="ce82e-109">Azure Remote App</span></span>
* <span data-ttu-id="ce82e-110">Aplicativos de linha de negócios e de multilocação desenvolvidos registrados no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ce82e-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="ce82e-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="ce82e-111">Dynamics CRM</span></span>
* <span data-ttu-id="ce82e-112">Aplicativos federados da Galeria de aplicativo do AD do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="ce82e-112">Federated applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="ce82e-113">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="ce82e-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="ce82e-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="ce82e-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="ce82e-115">Microsoft Office 365 SharePoint Online (inclui o OneDrive for Business)</span><span class="sxs-lookup"><span data-stu-id="ce82e-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="ce82e-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="ce82e-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="ce82e-117">Aplicativos de SSO de senha da Galeria de aplicativo hello AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ce82e-117">Password SSO applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="ce82e-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="ce82e-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="ce82e-119">Equipes da Microsoft</span><span class="sxs-lookup"><span data-stu-id="ce82e-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="ce82e-120">Habilitar regras de acesso</span><span class="sxs-lookup"><span data-stu-id="ce82e-120">Enable access rules</span></span>
<span data-ttu-id="ce82e-121">Cada regra pode ser habilitada ou desabilitada com base no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce82e-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="ce82e-122">Quando as regras são **ON** serão habilitadas e aplicadas a usuários que acessam o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ce82e-122">When rules are **ON** they will be enabled and enforced for users accessing hello application.</span></span> <span data-ttu-id="ce82e-123">Quando eles são **OFF** não serão usados e assinará não usuários de saudação do impacto na experiência.</span><span class="sxs-lookup"><span data-stu-id="ce82e-123">When they are **OFF** they will not be used and will not impact hello users sign in experience.</span></span>

## <a name="applying-rules-toospecific-users"></a><span data-ttu-id="ce82e-124">Usuários de toospecific aplicando regras</span><span class="sxs-lookup"><span data-stu-id="ce82e-124">Applying rules toospecific users</span></span>
<span data-ttu-id="ce82e-125">As regras podem ser aplicadas toospecific conjuntos de usuários com base no grupo de segurança, definindo **aplicar a**.</span><span class="sxs-lookup"><span data-stu-id="ce82e-125">Rules can be applied toospecific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="ce82e-126">**Aplicar a** pode ser definido muito**todos os usuários** ou **grupos**.</span><span class="sxs-lookup"><span data-stu-id="ce82e-126">**Apply To** can be set too**All Users** or **Groups**.</span></span> <span data-ttu-id="ce82e-127">Quando definido muito**todos os usuários** Olá regras se aplicarão tooany usuário com aplicativos de toohello de acesso.</span><span class="sxs-lookup"><span data-stu-id="ce82e-127">When set too**All Users** hello rules will apply tooany user with access toohello application.</span></span> <span data-ttu-id="ce82e-128">Olá **grupos** opção permite específicas de segurança e toobe de grupos de distribuição selecionado, as regras serão aplicadas apenas para esses grupos.</span><span class="sxs-lookup"><span data-stu-id="ce82e-128">hello **Groups** option allows specific security and distribution groups toobe selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="ce82e-129">Ao implantar uma regra, é comum toofirst aplicá-lo um conjunto limitado de usuários, que são membros de grupos um piloto.</span><span class="sxs-lookup"><span data-stu-id="ce82e-129">When deploying a rule,  it is common toofirst apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="ce82e-130">Depois que a regra de saudação completa pode ser aplicada muito**todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="ce82e-130">Once complete hello rule can be applied too**All Users**.</span></span> <span data-ttu-id="ce82e-131">Isso fará com que a regra Olá toobe imposta para todos os usuários na organização hello.</span><span class="sxs-lookup"><span data-stu-id="ce82e-131">This will cause hello rule toobe enforced for all users in hello organization.</span></span>

<span data-ttu-id="ce82e-132">Selecione grupos também podem ser isentos da política usando Olá **exceto** opção.</span><span class="sxs-lookup"><span data-stu-id="ce82e-132">Select groups may also be exempted from policy using hello **Except** option.</span></span> <span data-ttu-id="ce82e-133">Todos os membros desses grupos estarão isentos mesmo que apareçam em um grupo incluído.</span><span class="sxs-lookup"><span data-stu-id="ce82e-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="ce82e-134">Redes "No trabalho"</span><span class="sxs-lookup"><span data-stu-id="ce82e-134">“At work” networks</span></span>
<span data-ttu-id="ce82e-135">As regras de acesso condicional que usam uma rede "no trabalho", dependem de intervalos de endereços IP confiáveis que foram configurados no AD do Azure, ou o uso de hello "dentro da rede corporativa" declarações do AD FS.</span><span class="sxs-lookup"><span data-stu-id="ce82e-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of hello "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="ce82e-136">Essas regras incluem:</span><span class="sxs-lookup"><span data-stu-id="ce82e-136">These rules include:</span></span>

* <span data-ttu-id="ce82e-137">Exigir autenticação multifator quando não está no trabalho</span><span class="sxs-lookup"><span data-stu-id="ce82e-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="ce82e-138">Bloquear acesso quando não estiver no trabalho</span><span class="sxs-lookup"><span data-stu-id="ce82e-138">Block access when not at work</span></span>

<span data-ttu-id="ce82e-139">Opções para especificar redes "no trabalho"</span><span class="sxs-lookup"><span data-stu-id="ce82e-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="ce82e-140">Configurar intervalos de endereços IP confiáveis em hello [página de configuração de autenticação multifator](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="ce82e-140">Configure trusted IP address ranges in hello [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="ce82e-141">Política de acesso condicional usará os intervalos de saudação configurado em cada solicitação e o token de emissão tooevaluate as regras de autenticação.</span><span class="sxs-lookup"><span data-stu-id="ce82e-141">Conditional Access policy will use hello configured ranges on each authentication request and token issuance tooevaluate rules.</span></span> 
2. <span data-ttu-id="ce82e-142">Configurar o uso de saudação dentro de declaração da rede corporativa, essa opção pode ser usada com diretórios federados, usando o AD FS.</span><span class="sxs-lookup"><span data-stu-id="ce82e-142">Configure use of hello inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="ce82e-143">toolearn mais sobre hello dentro de declarações de rede corporativa, consulte [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="ce82e-143">toolearn more about hello inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="ce82e-144">Regras com base na confidencialidade do aplicativo</span><span class="sxs-lookup"><span data-stu-id="ce82e-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="ce82e-145">Regras são configuradas por aplicativo permitindo Olá alto valor serviços toobe protegida sem afetar o acesso tooother serviços.</span><span class="sxs-lookup"><span data-stu-id="ce82e-145">Rules are configured per application allowing hello high value services toobe secured without impacting access tooother services.</span></span> <span data-ttu-id="ce82e-146">Regras de acesso condicional podem ser configuradas em Olá **configurar** guia do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ce82e-146">Conditional access rules can be configured on hello  **Configure** tab of hello application.</span></span> 

<span data-ttu-id="ce82e-147">Regras oferecidas atualmente:</span><span class="sxs-lookup"><span data-stu-id="ce82e-147">Rules currently offered:</span></span>

* <span data-ttu-id="ce82e-148">**Exigir autenticação multifator**</span><span class="sxs-lookup"><span data-stu-id="ce82e-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="ce82e-149">Todos os usuários que essa política é aplicada toowill ser tooauthenticate necessária por meio de pelo menos uma vez a autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="ce82e-149">All users that this policy is applied toowill be required tooauthenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="ce82e-150">**Exigir autenticação multifator quando não está no trabalho**</span><span class="sxs-lookup"><span data-stu-id="ce82e-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="ce82e-151">Se essa política é aplicada, todos os usuários serão autenticação de multifator toohave necessária executada pelo menos uma vez se acessam o serviço de saudação de um local remoto inativo.</span><span class="sxs-lookup"><span data-stu-id="ce82e-151">If this policy is applied, all users will be required toohave performed multi-factor authentication at least once if they access hello service from a non-work remote location.</span></span> <span data-ttu-id="ce82e-152">Se eles mudam de local de tooremote um trabalho, eles serão tooperform necessária a autenticação multifator ao acessar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce82e-152">If they move from a work tooremote location, they will be required tooperform multifactor authentication when accessing hello service.</span></span>
* <span data-ttu-id="ce82e-153">**Bloquear acesso quando não estiver no trabalho**</span><span class="sxs-lookup"><span data-stu-id="ce82e-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="ce82e-154">Quando os usuários mudam de local remoto do trabalho tooa, eles serão bloqueados se hello, "Bloquear acesso quando não estiver no trabalho" política é aplicada toothem.</span><span class="sxs-lookup"><span data-stu-id="ce82e-154">When users move from work tooa remote location, they will be blocked if hello "Block access when not at work" policy is applied toothem.</span></span>  <span data-ttu-id="ce82e-155">Eles terão o acesso permitido novamente quando estiverem em um local de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ce82e-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="ce82e-156">Tópicos relacionados</span><span class="sxs-lookup"><span data-stu-id="ce82e-156">Related topics</span></span>
* [<span data-ttu-id="ce82e-157">Protegendo o acesso tooOffice 365 e outros aplicativos conectados tooAzure do Active Directory</span><span class="sxs-lookup"><span data-stu-id="ce82e-157">Securing access tooOffice 365 and other apps connected tooAzure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="ce82e-158">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ce82e-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

