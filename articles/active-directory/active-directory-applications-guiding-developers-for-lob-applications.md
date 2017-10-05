---
title: Desenvolver aplicativos para o Azure AD| Microsoft Docs
description: "Escrito para profissionais de TI, este artigo fornece diretrizes para a integração de aplicativos do Azure com o Active Directory."
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
ms.openlocfilehash: 6b119be9c06d8c1ccc8e747168429e6c2d2e7a8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="a085c-103">Desenvolver aplicativos de linha de negócios para o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a085c-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="a085c-104">Este guia fornece uma visão geral do desenvolvimento de aplicativos LoB (de linha de negócios) do Azure AD (Active Directory). O público-alvo são os administradores globais do Active Directory/Office 365.</span><span class="sxs-lookup"><span data-stu-id="a085c-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).The intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="a085c-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a085c-105">Overview</span></span>
<span data-ttu-id="a085c-106">A criação de aplicativos integrados ao AD do Azure oferece aos usuários em sua organização logon único com o Office 365.</span><span class="sxs-lookup"><span data-stu-id="a085c-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="a085c-107">Ter o aplicativo no Azure AD dá controle sobre a política de autenticação definida para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a085c-107">Having the application in Azure AD gives you control over the authentication policy for the application.</span></span> <span data-ttu-id="a085c-108">Para saber mais sobre acesso condicional e como proteger aplicativos com MFA (Multi-Factor Authentication), consulte [Configurando regras de acesso](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="a085c-108">To learn more about conditional access and how to protect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="a085c-109">Registre seu aplicativo com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a085c-109">Register your application to use Azure Active Directory.</span></span> <span data-ttu-id="a085c-110">Registrar o aplicativo significa que seus desenvolvedores podem usar o Azure AD para autenticar usuários e solicitar acesso a recursos de usuário como email, calendário e documentos.</span><span class="sxs-lookup"><span data-stu-id="a085c-110">Registering the application means that your developers can use Azure AD to authenticate users and request access to user resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="a085c-111">Qualquer membro do diretório (não convidados) pode registrar um aplicativo, também conhecido como *criação de um objeto de aplicativo*.</span><span class="sxs-lookup"><span data-stu-id="a085c-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="a085c-112">Registrar um aplicativo permite que qualquer usuário faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a085c-112">Registering an application allows any user to do the following:</span></span>

* <span data-ttu-id="a085c-113">Obter uma identidade para o aplicativo que reconhece o AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a085c-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="a085c-114">Obter um ou mais segredos/chaves que o aplicativo pode usar para se autenticar no AD</span><span class="sxs-lookup"><span data-stu-id="a085c-114">Get one or more secrets/keys that the application can use to authenticate itself to AD</span></span>
* <span data-ttu-id="a085c-115">Marcar o aplicativo no portal do Azure com um nome, logotipo personalizado etc.</span><span class="sxs-lookup"><span data-stu-id="a085c-115">Brand the application in the Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="a085c-116">Aproveitar os recursos de autorização do Azure AD para seu aplicativo, incluindo:</span><span class="sxs-lookup"><span data-stu-id="a085c-116">Apply Azure AD authorization features to their app, including:</span></span>

  * <span data-ttu-id="a085c-117">RBAC (Controle de Acesso Baseado em Função)</span><span class="sxs-lookup"><span data-stu-id="a085c-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="a085c-118">Active Directory do Azure como servidor de autorização oAuth (proteger uma API exposta pelo aplicativo)</span><span class="sxs-lookup"><span data-stu-id="a085c-118">Azure Active Directory as oAuth authorization server (secure an API exposed by the application)</span></span>
* <span data-ttu-id="a085c-119">Declarar as permissões exigidas necessárias para que o aplicativo funcione conforme o esperado, incluindo:</span><span class="sxs-lookup"><span data-stu-id="a085c-119">Declare required permissions necessary for the application to function as expected, including:</span></span>

      - <span data-ttu-id="a085c-120">Permissões de aplicativo (somente administradores globais).</span><span class="sxs-lookup"><span data-stu-id="a085c-120">App permissions (global administrators only).</span></span> <span data-ttu-id="a085c-121">Por exemplo: associação de função em outro aplicativo do Azure AD ou associação de grupo relativa a um recurso, grupo de recursos ou assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="a085c-121">For example: Role membership in another Azure AD application or role membership relative to an Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="a085c-122">Permissões (qualquer usuário).</span><span class="sxs-lookup"><span data-stu-id="a085c-122">Delegated permissions (any user).</span></span> <span data-ttu-id="a085c-123">Por exemplo: Azure AD, Entrar e Ler o Perfil</span><span class="sxs-lookup"><span data-stu-id="a085c-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="a085c-124">Por padrão, qualquer membro pode registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a085c-124">By default, any member can register an application.</span></span> <span data-ttu-id="a085c-125">Para saber como restringir as permissões para o registro de aplicativos para membros específicos, consulte [Como os aplicativos são adicionados ao Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span><span class="sxs-lookup"><span data-stu-id="a085c-125">To learn how to restrict permissions for registering applications to specific members, see [How applications are added to Azure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="a085c-126">Aqui está o que você, o administrador global, precisa fazer para ajudar os desenvolvedores a preparar o aplicativo para produção:</span><span class="sxs-lookup"><span data-stu-id="a085c-126">Here’s what you, the global administrator, need to do to help developers make their application ready for production:</span></span>

* <span data-ttu-id="a085c-127">Configurar regras de acesso (política de acesso/MFA)</span><span class="sxs-lookup"><span data-stu-id="a085c-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="a085c-128">Configurar o aplicativo para exigir a atribuição de usuário e atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="a085c-128">Configure the app to require user assignment and assign users</span></span>
* <span data-ttu-id="a085c-129">Suprimir a experiência de consentimento do usuário padrão</span><span class="sxs-lookup"><span data-stu-id="a085c-129">Suppress the default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="a085c-130">Configurar regras de acesso</span><span class="sxs-lookup"><span data-stu-id="a085c-130">Configure access rules</span></span>
<span data-ttu-id="a085c-131">Configurar regras de acesso por aplicativo para seus aplicativos de SaaS.</span><span class="sxs-lookup"><span data-stu-id="a085c-131">Configure per-application access rules to your SaaS apps.</span></span> <span data-ttu-id="a085c-132">Por exemplo você pode exigir MFA ou somente permitir o acesso a usuários em redes confiáveis.</span><span class="sxs-lookup"><span data-stu-id="a085c-132">For example, you can require MFA or only allow access to users on trusted networks.</span></span> <span data-ttu-id="a085c-133">Os detalhes para isso estão disponíveis no documento [Configurando regras de acesso](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="a085c-133">The details for this are available in the document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-the-app-to-require-user-assignment-and-assign-users"></a><span data-ttu-id="a085c-134">Configurar o aplicativo para exigir a atribuição de usuário e atribuir usuários</span><span class="sxs-lookup"><span data-stu-id="a085c-134">Configure the app to require user assignment and assign users</span></span>
<span data-ttu-id="a085c-135">Por padrão, os usuários podem acessar aplicativos sem ser atribuídos.</span><span class="sxs-lookup"><span data-stu-id="a085c-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="a085c-136">No entanto, se o aplicativo expõe funções ou se você deseja que o aplicativo seja exibido no painel de acesso do usuário, você deve exigir a atribuição de usuário.</span><span class="sxs-lookup"><span data-stu-id="a085c-136">However, if the application exposes roles or if you want the application to appear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="a085c-137">Exigindo atribuição do usuário</span><span class="sxs-lookup"><span data-stu-id="a085c-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="a085c-138">Caso você seja um assinante do Azure AD Premium ou EMS (Enterprise Mobility Suite), é altamente recomendável usar grupos.</span><span class="sxs-lookup"><span data-stu-id="a085c-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="a085c-139">A atribuição de grupos ao aplicativo permite delegar o gerenciamento de acesso contínuo ao proprietário do grupo.</span><span class="sxs-lookup"><span data-stu-id="a085c-139">Assigning groups to the application allows you to delegate ongoing access management to the owner of the group.</span></span> <span data-ttu-id="a085c-140">Você pode criar o grupo ou, se preferir, pedir à parte responsável da sua organização para criar o grupo usando o recurso de gerenciamento de grupos.</span><span class="sxs-lookup"><span data-stu-id="a085c-140">You can create the group or ask the responsible party in your organization to create the group using your group management facility.</span></span>

[<span data-ttu-id="a085c-141">Atribuindo usuários a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="a085c-141">Assigning users to an application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="a085c-142">Atribuindo grupos a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="a085c-142">Assigning groups to an application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="a085c-143">Suprimir o consentimento do usuário</span><span class="sxs-lookup"><span data-stu-id="a085c-143">Suppress user consent</span></span>
<span data-ttu-id="a085c-144">Por padrão, cada usuário passa por uma experiência de consentimento para entrar.</span><span class="sxs-lookup"><span data-stu-id="a085c-144">By default, each user goes through a consent experience to sign in.</span></span> <span data-ttu-id="a085c-145">A experiência de consentimento, de ser solicitado a conceder permissões para um aplicativo, pode ser desconcertante para usuários que não estão familiarizados com essa decisão.</span><span class="sxs-lookup"><span data-stu-id="a085c-145">The consent experience, asking users to grant permissions to an application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="a085c-146">Para aplicativos em que você confia, você pode simplificar a experiência do usuário consentindo aplicativo em nome de sua organização.</span><span class="sxs-lookup"><span data-stu-id="a085c-146">For applications that you trust, you can simplify the user experience by consenting to the application on behalf of your organization.</span></span>

<span data-ttu-id="a085c-147">Para saber mais sobre o consentimento do usuário e sobre a experiência de consentimento no Azure, confira [Integrando aplicativos com o Azure Active Directory](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="a085c-147">For more information about user consent and the consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="a085c-148">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="a085c-148">Related Articles</span></span>
* [<span data-ttu-id="a085c-149">Habilitar acesso remoto seguro a aplicativos locais com o Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a085c-149">Enable secure remote access to on-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="a085c-150">Visualização de acesso condicional do Azure para aplicativos SaaS</span><span class="sxs-lookup"><span data-stu-id="a085c-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="a085c-151">Gerenciando o acesso a aplicativos usando o Azure AD</span><span class="sxs-lookup"><span data-stu-id="a085c-151">Managing access to apps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="a085c-152">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a085c-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
