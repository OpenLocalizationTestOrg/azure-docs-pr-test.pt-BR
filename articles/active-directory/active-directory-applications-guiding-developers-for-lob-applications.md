---
title: aplicativos de aaaDevelop do AD do Azure | Microsoft Docs
description: "Escrito para Olá profissional de TI, este artigo fornece diretrizes para a integração de aplicativos do Azure com o Active Directory."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="10871-103">Desenvolver aplicativos de linha de negócios para o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="10871-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="10871-104">Este guia fornece uma visão geral do desenvolvimento de aplicativos do linha de negócios (LoB) para o Azure AD (Active Directory) .hello deve público é que os administradores globais do Active Directory/Office 365.</span><span class="sxs-lookup"><span data-stu-id="10871-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).hello intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="10871-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="10871-105">Overview</span></span>
<span data-ttu-id="10871-106">A criação de aplicativos integrados ao AD do Azure oferece aos usuários em sua organização logon único com o Office 365.</span><span class="sxs-lookup"><span data-stu-id="10871-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="10871-107">Com o aplicativo hello no AD do Azure lhe dá que controle sobre a política de autenticação Olá para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="10871-107">Having hello application in Azure AD gives you control over hello authentication policy for hello application.</span></span> <span data-ttu-id="10871-108">toolearn mais sobre acesso condicional e como aplicativos de tooprotect com autenticação multifator (MFA), consulte [Configurando regras de acesso](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="10871-108">toolearn more about conditional access and how tooprotect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="10871-109">Registre seu toouse de aplicativo do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="10871-109">Register your application toouse Azure Active Directory.</span></span> <span data-ttu-id="10871-110">Registrar o aplicativo hello significa que os desenvolvedores podem usar usuários do AD do Azure tooauthenticate e solicitar acesso toouser recursos como email, calendário e documentos.</span><span class="sxs-lookup"><span data-stu-id="10871-110">Registering hello application means that your developers can use Azure AD tooauthenticate users and request access toouser resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="10871-111">Qualquer membro do diretório (não convidados) pode registrar um aplicativo, também conhecido como *criação de um objeto de aplicativo*.</span><span class="sxs-lookup"><span data-stu-id="10871-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="10871-112">Registrar um aplicativo permite que qualquer usuário toodo Olá das seguintes:</span><span class="sxs-lookup"><span data-stu-id="10871-112">Registering an application allows any user toodo hello following:</span></span>

* <span data-ttu-id="10871-113">Obter uma identidade para o aplicativo que reconhece o AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10871-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="10871-114">Obtenha uma ou mais segredos/chaves que Olá aplicativo pode usar tooauthenticate próprio tooAD</span><span class="sxs-lookup"><span data-stu-id="10871-114">Get one or more secrets/keys that hello application can use tooauthenticate itself tooAD</span></span>
* <span data-ttu-id="10871-115">Aplicativo de hello marca no hello portal do Azure com um nome personalizado, logotipo, etc.</span><span class="sxs-lookup"><span data-stu-id="10871-115">Brand hello application in hello Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="10871-116">Aplicar o aplicativo de tootheir de recursos de autorização do AD do Azure, incluindo:</span><span class="sxs-lookup"><span data-stu-id="10871-116">Apply Azure AD authorization features tootheir app, including:</span></span>

  * <span data-ttu-id="10871-117">RBAC (Controle de Acesso Baseado em Função)</span><span class="sxs-lookup"><span data-stu-id="10871-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="10871-118">Azure Active Directory como servidor de autorização do oAuth (proteger uma API exposta pelo aplicativo hello)</span><span class="sxs-lookup"><span data-stu-id="10871-118">Azure Active Directory as oAuth authorization server (secure an API exposed by hello application)</span></span>
* <span data-ttu-id="10871-119">Declare permissões exigidas necessárias para toofunction de aplicativo hello conforme o esperado, incluindo:</span><span class="sxs-lookup"><span data-stu-id="10871-119">Declare required permissions necessary for hello application toofunction as expected, including:</span></span>

      - <span data-ttu-id="10871-120">Permissões de aplicativo (somente administradores globais).</span><span class="sxs-lookup"><span data-stu-id="10871-120">App permissions (global administrators only).</span></span> <span data-ttu-id="10871-121">Por exemplo: associação de função no outro AD do Azure aplicativo ou função de associação relativo tooan Azure recursos, grupo de recursos, ou a assinatura</span><span class="sxs-lookup"><span data-stu-id="10871-121">For example: Role membership in another Azure AD application or role membership relative tooan Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="10871-122">Permissões (qualquer usuário).</span><span class="sxs-lookup"><span data-stu-id="10871-122">Delegated permissions (any user).</span></span> <span data-ttu-id="10871-123">Por exemplo: Azure AD, Entrar e Ler o Perfil</span><span class="sxs-lookup"><span data-stu-id="10871-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="10871-124">Por padrão, qualquer membro pode registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="10871-124">By default, any member can register an application.</span></span> <span data-ttu-id="10871-125">toolearn como toorestrict permissões para registrar os membros de toospecific de aplicativos, consulte [como os aplicativos são adicionados tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span><span class="sxs-lookup"><span data-stu-id="10871-125">toolearn how toorestrict permissions for registering applications toospecific members, see [How applications are added tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="10871-126">Aqui está o que você, administrador global hello, precisam toodo toohelp desenvolvedores tornar seu aplicativo pronto para produção:</span><span class="sxs-lookup"><span data-stu-id="10871-126">Here’s what you, hello global administrator, need toodo toohelp developers make their application ready for production:</span></span>

* <span data-ttu-id="10871-127">Configurar regras de acesso (política de acesso/MFA)</span><span class="sxs-lookup"><span data-stu-id="10871-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="10871-128">Configurar aplicativo hello de toorequire atribuição de usuário e atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="10871-128">Configure hello app toorequire user assignment and assign users</span></span>
* <span data-ttu-id="10871-129">Suprimir a experiência de consentimento do usuário saudação padrão</span><span class="sxs-lookup"><span data-stu-id="10871-129">Suppress hello default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="10871-130">Configurar regras de acesso</span><span class="sxs-lookup"><span data-stu-id="10871-130">Configure access rules</span></span>
<span data-ttu-id="10871-131">Configure aplicativos de SaaS de tooyour de regras de acesso por aplicativo.</span><span class="sxs-lookup"><span data-stu-id="10871-131">Configure per-application access rules tooyour SaaS apps.</span></span> <span data-ttu-id="10871-132">Por exemplo, você pode exigir a MFA ou permitir apenas acesso toousers em redes confiáveis.</span><span class="sxs-lookup"><span data-stu-id="10871-132">For example, you can require MFA or only allow access toousers on trusted networks.</span></span> <span data-ttu-id="10871-133">detalhes de saudação para este estão disponíveis no documento hello [Configurando regras de acesso](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="10871-133">hello details for this are available in hello document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a><span data-ttu-id="10871-134">Configurar aplicativo hello de toorequire atribuição de usuário e atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="10871-134">Configure hello app toorequire user assignment and assign users</span></span>
<span data-ttu-id="10871-135">Por padrão, os usuários podem acessar aplicativos sem ser atribuídos.</span><span class="sxs-lookup"><span data-stu-id="10871-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="10871-136">No entanto, se o aplicativo hello expõe funções ou se você quiser que o hello tooappear de aplicativo no painel de acesso do usuário, você deve exigir a atribuição do usuário.</span><span class="sxs-lookup"><span data-stu-id="10871-136">However, if hello application exposes roles or if you want hello application tooappear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="10871-137">Exigindo atribuição do usuário</span><span class="sxs-lookup"><span data-stu-id="10871-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="10871-138">Caso você seja um assinante do Azure AD Premium ou EMS (Enterprise Mobility Suite), é altamente recomendável usar grupos.</span><span class="sxs-lookup"><span data-stu-id="10871-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="10871-139">Atribuir grupos toohello aplicativo permite que você toodelegate acesso contínuo gerenciamento toohello proprietário do grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="10871-139">Assigning groups toohello application allows you toodelegate ongoing access management toohello owner of hello group.</span></span> <span data-ttu-id="10871-140">Você pode criar um grupo de saudação ou fazer parte responsável Olá em sua organização toocreate Olá grupo usando o recurso de gerenciamento de grupo.</span><span class="sxs-lookup"><span data-stu-id="10871-140">You can create hello group or ask hello responsible party in your organization toocreate hello group using your group management facility.</span></span>

[<span data-ttu-id="10871-141">Atribuir usuários tooan aplicativo</span><span class="sxs-lookup"><span data-stu-id="10871-141">Assigning users tooan application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="10871-142">Atribuir grupos de aplicativo tooan</span><span class="sxs-lookup"><span data-stu-id="10871-142">Assigning groups tooan application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="10871-143">Suprimir o consentimento do usuário</span><span class="sxs-lookup"><span data-stu-id="10871-143">Suppress user consent</span></span>
<span data-ttu-id="10871-144">Por padrão, cada usuário passa por um toosign de experiência de consentimento no.</span><span class="sxs-lookup"><span data-stu-id="10871-144">By default, each user goes through a consent experience toosign in.</span></span> <span data-ttu-id="10871-145">experiência de consentimento Hello, solicitando permissões a usuários toogrant tooan aplicativo, pode ser desconcertante para usuários que não estão familiarizados com essas decisões.</span><span class="sxs-lookup"><span data-stu-id="10871-145">hello consent experience, asking users toogrant permissions tooan application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="10871-146">Para aplicativos que você confia, você pode simplificar a experiência do usuário de saudação pelo aplicativo de toohello consentimento em nome de sua organização.</span><span class="sxs-lookup"><span data-stu-id="10871-146">For applications that you trust, you can simplify hello user experience by consenting toohello application on behalf of your organization.</span></span>

<span data-ttu-id="10871-147">Para obter mais informações sobre o consentimento do usuário e o consentimento de saudação experiência no Azure, consulte [integrando aplicativos com o Active Directory do Azure](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="10871-147">For more information about user consent and hello consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="10871-148">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="10871-148">Related Articles</span></span>
* [<span data-ttu-id="10871-149">Habilitar acesso remoto seguro local tooon aplicativos com Proxy de aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="10871-149">Enable secure remote access tooon-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="10871-150">Visualização de acesso condicional do Azure para aplicativos SaaS</span><span class="sxs-lookup"><span data-stu-id="10871-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="10871-151">Gerenciando acesso tooapps com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="10871-151">Managing access tooapps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="10871-152">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="10871-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
