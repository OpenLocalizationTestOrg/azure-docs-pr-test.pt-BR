---
title: "aaaHow toodetermine o logon único no método toouse | Microsoft Docs"
description: "Entender Olá único logon modos suportados pelo AD do Azure e como toopick quais um toochoose para Olá aplicativo que lhe interessam."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 64f0bc1dc8281d1ab8222fd50eaceaf710704886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetermine-what-single-sign-on-method-toouse"></a><span data-ttu-id="d9d28-103">Como toodetermine o logon único no método toouse</span><span class="sxs-lookup"><span data-stu-id="d9d28-103">How toodetermine what single-sign on method toouse</span></span>

<span data-ttu-id="d9d28-104">Este artigo ajuda toounderstand Olá único logon modos suportados pelo AD do Azure e como toopick quais um toochoose para Olá aplicativo que lhe interessam.</span><span class="sxs-lookup"><span data-stu-id="d9d28-104">This article help you toounderstand hello single sign-on modes supported by Azure AD and how toopick which one toochoose for hello application you are interested in.</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="d9d28-105">Modos de logon único e provisionamento com suporte de tipos específicos de aplicativos</span><span class="sxs-lookup"><span data-stu-id="d9d28-105">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="d9d28-106">Olá tabela a seguir descreve Olá diferentes logon único e provisionamento modos suportados por cada Olá acima tipos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d9d28-106">hello table below describes hello different single sign-on and provisioning modes supported by each of hello above application types.</span></span> <span data-ttu-id="d9d28-107">Você pode usar essa tabela toohelp toounderstand qual aplicativo precisar tooadd toosupport uma meta específica.</span><span class="sxs-lookup"><span data-stu-id="d9d28-107">You can use this table toohelp you toounderstand which application you need tooadd toosupport a specific goal.</span></span>

  ![Tabela de tipos de aplicativo](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a><span data-ttu-id="d9d28-109">Como toochoose um modo de logon único</span><span class="sxs-lookup"><span data-stu-id="d9d28-109">How toochoose a single sign-on mode</span></span>

<span data-ttu-id="d9d28-110">Olá suportada **o logon único** modos para aplicativos do Azure AD estão listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="d9d28-110">hello supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="d9d28-111">**Azure AD SSO desabilitado** – escolha AD do Azure SSO desabilitado **modo de logon único** se você ainda não está pronto toointegrate este aplicativo com logon único com o Azure AD ou são simplesmente experimentá-lo</span><span class="sxs-lookup"><span data-stu-id="d9d28-111">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready toointegrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="d9d28-112">**Vinculado logon** – escolha Olá [logon vinculado](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modo de logon único** se você tiver um aplicativo que já está conectado com uma único logon solução existente, ou se você quiser apenas toopublish simples de link para os usuários em seus [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) ou [iniciador do aplicativo Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="d9d28-112">**Linked Sign-on** – choose hello [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want toopublish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="d9d28-113">**Com base em senha de logon** – escolha Olá [baseada em senha logon](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modo de logon único** se seu aplicativo processa um campo de nome de usuário e senha do HTML e você desejar toostore que nome de usuário e senha repetido de toobe com segurança toohello aplicativo mais tarde</span><span class="sxs-lookup"><span data-stu-id="d9d28-113">**Password-based Sign-on** – choose hello [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want toostore that username and password securely toobe replayed toohello application later</span></span>

-   <span data-ttu-id="d9d28-114">**Baseado no SAML logon** – escolha Olá [baseado no SAML logon](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) toospecific funções de aplicativo de logon único no modo se seu aplicativo dá suporte a protocolos SAML ou OpenID Connect hello, ou toobe toomap capaz de usuários com base em regras que você definir no seu SAML declarações *(**Observação:** essa opção não está disponível quando o proxy de aplicativo hello está configurado para um aplicativo) *</span><span class="sxs-lookup"><span data-stu-id="d9d28-114">**SAML-based Sign-on** – choose hello [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports hello SAML or OpenID Connect protocols, or you want toobe able toomap users toospecific application roles based on rules you define in your SAML claims *(**Note:** this option is not available when hello application proxy is configured for an application)*</span></span>

-   <span data-ttu-id="d9d28-115">**Com base no cabeçalho de logon** – Escolha esta opção [com base no cabeçalho de logon](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) autenticação que você deseja tooperform de logon único no muito baseada em único modo de logon se você tiver um aplicativo usando PingAccess que dá suporte ao cabeçalho HTTP *(**Observação:** essa opção só está disponível quando o proxy de aplicativo hello e PingAccess está configurado para um aplicativo) *</span><span class="sxs-lookup"><span data-stu-id="d9d28-115">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish tooperform single-sign on too*(**Note:** this option is only available when hello application proxy and PingAccess is configured for an application)*</span></span>

-   <span data-ttu-id="d9d28-116">**Autenticação integrada do Windows** – escolha Olá [autenticação integrada do Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) de logon único modo ao expor um aplicativo WIA local que você deseja tooperform de logon único no muito*(*  *Observação:** essa opção só está disponível quando o proxy de aplicativo hello está configurado para um aplicativo) *</span><span class="sxs-lookup"><span data-stu-id="d9d28-116">**Integrated Windows Authentication** – choose hello [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish tooperform single-sign on too*(**Note:** this option is only available when hello application proxy is configured for an application)*</span></span>

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="d9d28-117">Modos de logon único para aplicativos personalizados</span><span class="sxs-lookup"><span data-stu-id="d9d28-117">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="d9d28-118">Aplicativos que você tiver personalizado desenvolvido por meio de saudação [aplicativo personalizado](#_Custom-Developed_Applications) experiência também oferece suporte para único logon modos adicionais não listados acima.</span><span class="sxs-lookup"><span data-stu-id="d9d28-118">Applications you have custom developed through hello [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="d9d28-119">Estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="d9d28-119">These include:</span></span>

-   <span data-ttu-id="d9d28-120">Logon baseado em [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code)</span><span class="sxs-lookup"><span data-stu-id="d9d28-120">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="d9d28-121">Logon baseado em [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code)</span><span class="sxs-lookup"><span data-stu-id="d9d28-121">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="d9d28-122">Logon baseado em [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html)</span><span class="sxs-lookup"><span data-stu-id="d9d28-122">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="d9d28-123">Logon baseado em [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference)</span><span class="sxs-lookup"><span data-stu-id="d9d28-123">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="d9d28-124">Saudação de leitura [guia do desenvolvedor do Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn mais informações sobre como o aplicativo toocreate um personalizado que dá suporte a esses único modos de logon.</span><span class="sxs-lookup"><span data-stu-id="d9d28-124">Read hello [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn more about how toocreate a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-tooset-an-applications-single-sign-on-mode"></a><span data-ttu-id="d9d28-125">Como um aplicativo de tooset do único modo de logon</span><span class="sxs-lookup"><span data-stu-id="d9d28-125">How tooset an application’s single sign-on mode</span></span>

<span data-ttu-id="d9d28-126">tooset um aplicativo **o logon único** modo, siga Olá instruções abaixo:</span><span class="sxs-lookup"><span data-stu-id="d9d28-126">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="d9d28-127">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="d9d28-127">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="d9d28-128">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="d9d28-128">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="d9d28-129">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="d9d28-129">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="d9d28-130">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="d9d28-130">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="d9d28-131">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d9d28-131">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="d9d28-132">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="d9d28-132">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="d9d28-133">Selecionar aplicativo hello deseja tooconfigure-logon único</span><span class="sxs-lookup"><span data-stu-id="d9d28-133">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="d9d28-134">Depois que o aplicativo hello carrega, clique em **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d9d28-134">Once hello application loads, click **Single sign-on** from hello application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9d28-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9d28-135">Next steps</span></span>
[<span data-ttu-id="d9d28-136">Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo</span><span class="sxs-lookup"><span data-stu-id="d9d28-136">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

