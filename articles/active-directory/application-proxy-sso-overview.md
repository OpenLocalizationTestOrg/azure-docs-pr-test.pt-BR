---
title: aaaManage SSO para o Proxy de aplicativo do Azure AD | Microsoft Docs
description: "Saiba mais sobre conceitos básicos de saudação do logon único com o Proxy de aplicativo"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: a278751a5cb1bf98c970a4e5d2eb3edc3b784096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a><span data-ttu-id="33011-103">Como o Proxy de Aplicativo do Azure AD fornece logon único?</span><span class="sxs-lookup"><span data-stu-id="33011-103">How does Azure AD Application Proxy provide single sign-on?</span></span>

<span data-ttu-id="33011-104">O logon único é um elemento fundamental do Proxy de Aplicativo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="33011-104">Single sign-on is a key element of Azure AD Application Proxy.</span></span>  <span data-ttu-id="33011-105">Ele fornece a melhor experiência de usuário Olá porque os usuários têm apenas toosign em tooAzure do Active Directory na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="33011-105">It provides hello best user experience because your users only have toosign in tooAzure Active Directory in hello cloud.</span></span> <span data-ttu-id="33011-106">Depois que eles autenticam tooAzure do Active Directory, o conector de Proxy de aplicativo hello manipula aplicativo local do hello autenticação toohello.</span><span class="sxs-lookup"><span data-stu-id="33011-106">Once they authenticate tooAzure Active Directory, hello Application Proxy connector handles hello authentication toohello on-premises application.</span></span> <span data-ttu-id="33011-107">aplicativo de back-end Hello não pode determinar a diferença de saudação entre um usuário remoto entrar por meio do Proxy de aplicativo e um uso comum em um dispositivo ingressado no domínio.</span><span class="sxs-lookup"><span data-stu-id="33011-107">hello backend application can't tell hello difference between a remote user signing in through Application Proxy and a regular use on a domain-joined device.</span></span> 

<span data-ttu-id="33011-108">toouse Active Directory do Azure para aplicativos tooyour de logon único, você precisa tooselect **Active Directory do Azure** como método de pré-autenticação hello.</span><span class="sxs-lookup"><span data-stu-id="33011-108">toouse Azure Active Directory for single sign-on tooyour applications, you need tooselect **Azure Active Directory** as hello pre-authentication method.</span></span> <span data-ttu-id="33011-109">Se você selecionar **passagem** , em seguida, os usuários não autenticar tooAzure do Active Directory em todos os, mas são direcionados toohello simples aplicativo.</span><span class="sxs-lookup"><span data-stu-id="33011-109">If you select **Passthrough** then your users don't authenticate tooAzure Active Directory at all, but are directed straight toohello application.</span></span> <span data-ttu-id="33011-110">Você pode configurar essa configuração quando você publica um aplicativo, ou navegue tooyour aplicativo hello portal do Azure e editar as configurações de Proxy de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="33011-110">You can configure this setting when you first publish an application, or navigate tooyour application in hello Azure portal and edit hello Application Proxy settings.</span></span> 

<span data-ttu-id="33011-111">toosee seu único opções de logon, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="33011-111">toosee your single sign-on options, follow these steps:</span></span>

1. <span data-ttu-id="33011-112">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="33011-112">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="33011-113">Navegue muito**Active Directory do Azure** > **aplicativos empresariais** > **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="33011-113">Navigate too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="33011-114">Olá selecione aplicativo cujo logon único opções você deseja toomanage.</span><span class="sxs-lookup"><span data-stu-id="33011-114">Select hello app whose single sign-on options you want toomanage.</span></span>
4. <span data-ttu-id="33011-115">Selecione **Logon único**.</span><span class="sxs-lookup"><span data-stu-id="33011-115">Select **Single sign-on**.</span></span>

   ![Menu suspenso de logon único](./media/application-proxy-sso-overview/single-sign-on-mode.png)

<span data-ttu-id="33011-117">menu suspenso de saudação mostra cinco opções para o aplicativo tooyour de logon único:</span><span class="sxs-lookup"><span data-stu-id="33011-117">hello dropdown menu shows five options for single sign-on tooyour application:</span></span>

* <span data-ttu-id="33011-118">Logon único do Azure AD desabilitado</span><span class="sxs-lookup"><span data-stu-id="33011-118">Azure AD single sign-on disabled</span></span>
* <span data-ttu-id="33011-119">Logon baseado em senha</span><span class="sxs-lookup"><span data-stu-id="33011-119">Password-based sign-on</span></span>
* <span data-ttu-id="33011-120">Logon vinculado</span><span class="sxs-lookup"><span data-stu-id="33011-120">Linked sign-on</span></span>
* <span data-ttu-id="33011-121">Autenticação Integrada do Windows</span><span class="sxs-lookup"><span data-stu-id="33011-121">Integrated Windows Authentication</span></span>
* <span data-ttu-id="33011-122">Logon baseado em cabeçalho</span><span class="sxs-lookup"><span data-stu-id="33011-122">Header-based sign-on</span></span>

## <a name="azure-ad-single-sign-on-disabled"></a><span data-ttu-id="33011-123">Logon único do Azure AD desabilitado</span><span class="sxs-lookup"><span data-stu-id="33011-123">Azure AD single sign-on disabled</span></span>

<span data-ttu-id="33011-124">Se você não quiser a integração do Active Directory do Azure toouse tooyour de logon único aplicativo, escolha **AD do Azure SSO desabilitado**.</span><span class="sxs-lookup"><span data-stu-id="33011-124">If you don't want toouse Azure Active Directory integration for single sign-on tooyour application, choose **Azure AD single sign-on disabled**.</span></span> <span data-ttu-id="33011-125">Com essa opção selecionada, os usuários podem ter de se autenticar duas vezes.</span><span class="sxs-lookup"><span data-stu-id="33011-125">With this option selected, your users may authenticate twice.</span></span> <span data-ttu-id="33011-126">Primeiro, eles autenticar tooAzure do Active Directory e, em seguida, entre no próprio aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="33011-126">First, they authenticate tooAzure Active Directory and then sign in toohello application itself.</span></span> 

<span data-ttu-id="33011-127">Essa opção é uma boa opção se seu aplicativo local não precisa tooauthenticate de usuários, mas você deseja tooadd Active Directory do Azure como uma camada de segurança de acesso remoto.</span><span class="sxs-lookup"><span data-stu-id="33011-127">This option is a good choice if your on-premises application doesn't require users tooauthenticate, but you want tooadd Azure Active Directory as a layer of security for remote access.</span></span> 

## <a name="password-based-sign-on"></a><span data-ttu-id="33011-128">Logon baseado em senha</span><span class="sxs-lookup"><span data-stu-id="33011-128">Password-based sign-on</span></span>

<span data-ttu-id="33011-129">Se você quiser toouse Active Directory do Azure como um cofre de senhas para os aplicativos no local, escolha **baseada em senha logon**.</span><span class="sxs-lookup"><span data-stu-id="33011-129">If you want toouse Azure Active Directory as a password vault for your on-premises applications, choose **Password-based sign-on**.</span></span> <span data-ttu-id="33011-130">Essa opção é uma boa escolha se o aplicativo autentica com uma combinação de nome de usuário e senha em vez de tokens de acesso ou cabeçalhos.</span><span class="sxs-lookup"><span data-stu-id="33011-130">This option is a good choice if your application authenticates with a username/password combo instead of access tokens or headers.</span></span> <span data-ttu-id="33011-131">Com baseado em senha de logon, os usuários precisam ter toosign de saudação do aplicativo toohello primeira vez que o acessarem.</span><span class="sxs-lookup"><span data-stu-id="33011-131">With password-based sign-on, your users need toosign in toohello application hello first time they access it.</span></span> <span data-ttu-id="33011-132">Depois disso, o Active Directory do Azure fornece Olá username e password em nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="33011-132">After that, Azure Active Directory supplies hello username and password on behalf of hello user.</span></span> 

<span data-ttu-id="33011-133">Para obter informações sobre a configuração de logon baseado em senha, consulte [Compartimentação de senhas para logon único com Proxy de Aplicativo](application-proxy-sso-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="33011-133">For information about setting up password-based sign-on, see [Password vaulting for single sign-on with Application Proxy](application-proxy-sso-azure-portal.md).</span></span>

## <a name="linked-sign-on"></a><span data-ttu-id="33011-134">Logon vinculado</span><span class="sxs-lookup"><span data-stu-id="33011-134">Linked sign-on</span></span>

<span data-ttu-id="33011-135">Se você já tiver uma solução de logon único configurada para as identidades locais, escolha **Logon vinculado**.</span><span class="sxs-lookup"><span data-stu-id="33011-135">If you already have a single sign-on solution set up for your on-premises identities, choose **Linked sign-on**.</span></span> <span data-ttu-id="33011-136">Essa opção permite soluções existentes de SSO do Active Directory do Azure tooleverage, mas ainda oferece aos usuários aplicativos de toohello de acesso remoto.</span><span class="sxs-lookup"><span data-stu-id="33011-136">This option enables Azure Active Directory tooleverage existing SSO solutions, but still gives your users remote access toohello application.</span></span> 

<span data-ttu-id="33011-137">Para obter informações sobre logon vinculado (antigamente conhecido como logon único existente), confira [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="33011-137">For information about linked sign-on (formally known as existing single sign-on), see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

## <a name="integrated-windows-authentication"></a><span data-ttu-id="33011-138">Autenticação Integrada do Windows</span><span class="sxs-lookup"><span data-stu-id="33011-138">Integrated Windows Authentication</span></span>

<span data-ttu-id="33011-139">Se seus aplicativos de locais usam Authentication(IWA) integrada do Windows ou se você quiser toouse a delegação restrita de Kerberos (KCD) para o logon único, escolha **autenticação integrada do Windows**.</span><span class="sxs-lookup"><span data-stu-id="33011-139">If your on-premises applications use Integrated Windows Authentication(IWA) or if you want toouse Kerberos Constrained Delegation (KCD) for single sign-on, choose **Integrated Windows Authentication**.</span></span> <span data-ttu-id="33011-140">Com essa opção, os usuários precisam apenas tooauthenticate tooAzure do Active Directory e, em seguida, o conector de Proxy de aplicativo hello representa Olá usuário tooget um token Kerberos e entrar no aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="33011-140">With this option, your users only need tooauthenticate tooAzure Active Directory, and then hello Application Proxy connector impersonates hello user tooget a Kerberos token and sign in toohello application.</span></span> 

<span data-ttu-id="33011-141">Para obter informações sobre como configurar a autenticação integrada do Windows, consulte [Delegação restrita de Kerberos para logon único com o Proxy de Aplicativo](active-directory-application-proxy-sso-using-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="33011-141">For information about setting up Integrated Windows Authentication, see [Kerberos Constrained Delegation for single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md).</span></span>

## <a name="header-based-sign-on"></a><span data-ttu-id="33011-142">Logon baseado em cabeçalho</span><span class="sxs-lookup"><span data-stu-id="33011-142">Header-based sign-on</span></span> 

<span data-ttu-id="33011-143">Se seus aplicativos usam cabeçalhos para autenticação, escolha **logon baseado em cabeçalho**.</span><span class="sxs-lookup"><span data-stu-id="33011-143">If your applications use headers for authentication, choose **Header-based sign-on**.</span></span> <span data-ttu-id="33011-144">Com essa opção, os usuários precisam apenas tooauthentication Olá Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="33011-144">With this option, your users only need tooauthentication hello Azure Active Directory.</span></span> <span data-ttu-id="33011-145">Parceiros da Microsoft com um serviço de autenticação de terceiros chamado PingAccess, que é convertido de token de acesso do Active Directory do Azure Olá em um formato de cabeçalho para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="33011-145">Microsoft partners with a third-party authentication service called PingAccess, which translated hello Azure Active Directory access token into a header format for hello application.</span></span> 

<span data-ttu-id="33011-146">Para obter informações sobre como configurar a autenticação baseada em cabeçalho, consulte [ Autenticação baseada em cabeçalho para logon único com o Proxy de Aplicativo](application-proxy-ping-access.md).</span><span class="sxs-lookup"><span data-stu-id="33011-146">For information about setting up header-based authentication, see [Header-based authentication for single sign-on with Application Proxy](application-proxy-ping-access.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="33011-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="33011-147">Next steps</span></span>

- [<span data-ttu-id="33011-148">Compartimentação de senhas para logon único com o Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="33011-148">Password vaulting for single sign-on with Application Proxy</span></span>](application-proxy-sso-azure-portal.md)
- [<span data-ttu-id="33011-149">Delegação restrita de Kerberos para logon único com o Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="33011-149">Kerberos Constrained Delegation for single sign-on with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
- [<span data-ttu-id="33011-150">Autenticação baseada em cabeçalho para logon único com o Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="33011-150">Header-based authentication for single sign-on with Application Proxy</span></span>](application-proxy-ping-access.md) 
