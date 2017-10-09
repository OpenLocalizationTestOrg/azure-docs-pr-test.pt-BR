---
title: toochoose aaaHow qual aplicativo digite toouse ao adicionar um aplicativo | Microsoft Docs
description: "Entender os tipos de saudação com suporte de aplicativos, você pode integrar com o AD do Azure e suas opções de configuração relacionados"
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
ms.openlocfilehash: 46e3672e7f5048b0fa54171f0fc169362c9d5ac6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a><span data-ttu-id="06cf9-103">Como toochoose qual aplicativo digite toouse ao adicionar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="06cf9-103">How toochoose which application type toouse when adding an application</span></span>

<span data-ttu-id="06cf9-104">Este artigo ajuda toounderstand Olá quatro tipos principais de aplicativos, você pode integrar com o Azure AD:</span><span class="sxs-lookup"><span data-stu-id="06cf9-104">This article help you toounderstand hello four main types of applications you can integrate with Azure AD:</span></span>

* <span data-ttu-id="06cf9-105">O que tem suporte em cada um deles</span><span class="sxs-lookup"><span data-stu-id="06cf9-105">What is supported by each of them</span></span>
* <span data-ttu-id="06cf9-106">Por que você escolheria cada aplicativo</span><span class="sxs-lookup"><span data-stu-id="06cf9-106">Why you might choose which application</span></span>
* <span data-ttu-id="06cf9-107">Como tooconfigure propriedades de núcleo do aplicativo desses, como usuários **provisionado**, ou o que **o logon único** toouse de tecnologia.</span><span class="sxs-lookup"><span data-stu-id="06cf9-107">How tooconfigure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology toouse.</span></span>

## <a name="supported-application-types-in-azure-ad"></a><span data-ttu-id="06cf9-108">Tipos de aplicativos com suporte no Azure AD</span><span class="sxs-lookup"><span data-stu-id="06cf9-108">Supported application types in Azure AD</span></span>

<span data-ttu-id="06cf9-109">Olá do Azure AD oferece suporte a quatro principais tipos de aplicativos que você pode adicionar usando **adicionar** recurso encontrado em **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="06cf9-109">Azure AD supports four main application types that you can add using hello **Add** feature found under **Enterprise Applications**.</span></span> <span data-ttu-id="06cf9-110">Estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="06cf9-110">These include:</span></span>

-   <span data-ttu-id="06cf9-111">**Aplicativos da Galeria do Azure AD** – um aplicativo que foi integrado previamente para logon único com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06cf9-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

-   <span data-ttu-id="06cf9-112">**Aplicativos de Proxy de aplicativo** – um aplicativo em execução no seu ambiente local que você deseja tooprovide segura de logon único tooexternally.</span><span class="sxs-lookup"><span data-stu-id="06cf9-112">**Application Proxy Applications** – An application running in your on-premises environment that you want tooprovide secure single-sign on tooexternally.</span></span>

-   <span data-ttu-id="06cf9-113">**Aplicativos personalizado** – Olá de um aplicativo que sua organização deseja toodevelop na plataforma de desenvolvimento de aplicativo do Azure AD, mas que talvez ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="06cf9-113">**Custom-developed Applications** – An application that your organization wishes toodevelop on hello Azure AD Application Development Platform, but that may not exist yet.</span></span>

-   <span data-ttu-id="06cf9-114">**Aplicativos inexistentes na Galeria** – traga seus aplicativos!</span><span class="sxs-lookup"><span data-stu-id="06cf9-114">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="06cf9-115">Qualquer link da web que você deseja, qualquer aplicativo que processa um campo de nome de usuário e senha, oferece suporte a protocolos SAML ou OpenID Connect ou oferece suporte a SCIM que você deseja toointegrate para logon único com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06cf9-115">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish toointegrate for single sign-on with Azure AD.</span></span>

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a><span data-ttu-id="06cf9-116">Recursos e recursos com suporte de todos os Olá acima tipos de aplicativos</span><span class="sxs-lookup"><span data-stu-id="06cf9-116">Features and capabilities supported by all hello above application types</span></span>

<span data-ttu-id="06cf9-117">Olá recursos a seguir têm suporte por qualquer Olá acima 4 tipos de aplicativo no AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="06cf9-117">hello following features are supported by any of hello above 4 application types in Azure AD:</span></span>

-   <span data-ttu-id="06cf9-118">**Início rápido** – familiarize-se rapidamente com um aplicativo executando [etapas simples de implantação](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span><span class="sxs-lookup"><span data-stu-id="06cf9-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span></span>

-   <span data-ttu-id="06cf9-119">**Gerenciamento de propriedades gerais** – obter um [deeplink direto](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) tooan aplicativo, [personalizar identidade visual Olá](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) de um aplicativo, ou [desativar aplicativo hello](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) para todos os usuários.</span><span class="sxs-lookup"><span data-stu-id="06cf9-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) tooan application, [customize hello branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable hello application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span></span>

-   <span data-ttu-id="06cf9-120">**Gerenciamento de usuário e grupo** – [atribuir](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) ou [remover](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) aplicativo tooan de usuários e grupos e, opcionalmente, atribua funções de aplicativo específicas de saudação esses usuários e grupos têm acesso ao</span><span class="sxs-lookup"><span data-stu-id="06cf9-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups tooan application, and optionally assign hello specific application roles these users and groups have access to</span></span>

-   <span data-ttu-id="06cf9-121">**Acesso de aplicativo de autoatendimento** – habilitar seu usuários toorequest [acesso de aplicativo de autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooan aplicativo de seu aplicativo acesso painéis adicionando um aplicativo diretamente ou [ ingressando em um grupo habilitado autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), opcionalmente, exigir a aprovação de negócios ao longo de saudação maneira</span><span class="sxs-lookup"><span data-stu-id="06cf9-121">**Self-service application access** – enable your users toorequest [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooan application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along hello way</span></span>

-   <span data-ttu-id="06cf9-122">**Logs de logon** – consulte [todos Olá aplicativo de tooan entradas](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), ou todos os seus aplicativos</span><span class="sxs-lookup"><span data-stu-id="06cf9-122">**Sign-in logs** – see [all hello sign-ins tooan application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span></span>

-   <span data-ttu-id="06cf9-123">**Logs de auditoria** – consulte [logs de auditoria sobre o aplicativo de tooan modificações detalhados](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), ou tooall seus aplicativos</span><span class="sxs-lookup"><span data-stu-id="06cf9-123">**Audit logs** – see [detailed audit logs about modifications tooan application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or tooall your applications</span></span>

-   <span data-ttu-id="06cf9-124">**Acesso condicional baseado em risco e** – defina poderosa [regras de acesso com base em condição](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) que são aplicadas quando os usuários tentam toosign no aplicativo específico tooa</span><span class="sxs-lookup"><span data-stu-id="06cf9-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt toosign in tooa specific application</span></span>

-   <span data-ttu-id="06cf9-125">**Permissões de exibição** – exibir qualquer Olá [OAuth2 permissões](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) um aplicativo tem acesso tooin seu diretório de um único local</span><span class="sxs-lookup"><span data-stu-id="06cf9-125">**Permissions view** – view any of hello [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access tooin your directory from a single place</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="06cf9-126">Modos de logon único e provisionamento com suporte de tipos específicos de aplicativos</span><span class="sxs-lookup"><span data-stu-id="06cf9-126">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="06cf9-127">Olá tabela a seguir descreve Olá diferentes logon único e provisionamento modos suportados por cada Olá acima tipos de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="06cf9-127">hello table below describes hello different single sign-on and provisioning modes supported by each of hello above application types.</span></span> <span data-ttu-id="06cf9-128">Você pode usar essa tabela toohelp toounderstand qual aplicativo precisar tooadd toosupport uma meta específica.</span><span class="sxs-lookup"><span data-stu-id="06cf9-128">You can use this table toohelp you toounderstand which application you need tooadd toosupport a specific goal.</span></span>

  ![Tabela de tipos de aplicativo](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a><span data-ttu-id="06cf9-130">Como toochoose um modo de logon único</span><span class="sxs-lookup"><span data-stu-id="06cf9-130">How toochoose a single sign-on mode</span></span>

<span data-ttu-id="06cf9-131">Olá suportada **o logon único** modos para aplicativos do Azure AD estão listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="06cf9-131">hello supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="06cf9-132">**Azure AD SSO desabilitado** – escolha AD do Azure SSO desabilitado **modo de logon único** se você ainda não está pronto toointegrate este aplicativo com logon único com o Azure AD ou são simplesmente experimentá-lo</span><span class="sxs-lookup"><span data-stu-id="06cf9-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready toointegrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="06cf9-133">**Vinculado logon** – escolha Olá [logon vinculado](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modo de logon único** se você tiver um aplicativo que já está conectado com uma único logon solução existente, ou se você quiser apenas toopublish simples de link para os usuários em seus [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) ou [iniciador do aplicativo Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="06cf9-133">**Linked Sign-on** – choose hello [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want toopublish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="06cf9-134">**Com base em senha de logon** – escolha Olá [baseada em senha logon](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modo de logon único** se seu aplicativo processa um campo de nome de usuário e senha do HTML e você desejar toostore que nome de usuário e senha repetido de toobe com segurança toohello aplicativo mais tarde</span><span class="sxs-lookup"><span data-stu-id="06cf9-134">**Password-based Sign-on** – choose hello [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want toostore that username and password securely toobe replayed toohello application later</span></span>

-   <span data-ttu-id="06cf9-135">**Baseado no SAML logon** – escolha Olá [baseado no SAML logon](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) toospecific funções de aplicativo de logon único no modo se seu aplicativo dá suporte a protocolos SAML ou OpenID Connect hello, ou toobe toomap capaz de usuários com base em regras que você definir no seu SAML declarações *</span><span class="sxs-lookup"><span data-stu-id="06cf9-135">**SAML-based Sign-on** – choose hello [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports hello SAML or OpenID Connect protocols, or you want toobe able toomap users toospecific application roles based on rules you define in your SAML claims *</span></span>

   >[!NOTE]
   ><span data-ttu-id="06cf9-136">Essa opção não está disponível quando o proxy de aplicativo hello está configurado para um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="06cf9-136">This option is not available when hello application proxy is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="06cf9-137">**Com base no cabeçalho de logon** – Escolha esta opção [com base no cabeçalho de logon](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) autenticação que você deseja tooperform de logon único no muito baseada em único modo de logon se você tiver um aplicativo usando PingAccess que dá suporte ao cabeçalho HTTP</span><span class="sxs-lookup"><span data-stu-id="06cf9-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish tooperform single-sign on too</span></span>

   >[!NOTE]
   ><span data-ttu-id="06cf9-138">Essa opção só está disponível quando o proxy de aplicativo hello e PingAccess está configurado para um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="06cf9-138">This option is only available when hello application proxy and PingAccess is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="06cf9-139">**Autenticação integrada do Windows** – escolha Olá [autenticação integrada do Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) em modo ao expor um aplicativo WIA local que você deseja tooperform de logon único no muito do logon único</span><span class="sxs-lookup"><span data-stu-id="06cf9-139">**Integrated Windows Authentication** – choose hello [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish tooperform single-sign on too</span></span>

   >[!NOTE]
   ><span data-ttu-id="06cf9-140">Essa opção só está disponível quando o proxy de aplicativo hello está configurado para um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="06cf9-140">This option is only available when hello application proxy is configured for an application.</span></span>
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="06cf9-141">Modos de logon único para aplicativos personalizados</span><span class="sxs-lookup"><span data-stu-id="06cf9-141">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="06cf9-142">Aplicativos que você tiver personalizado desenvolvido por meio de saudação [aplicativo personalizado](#_Custom-Developed_Applications) experiência também oferece suporte para único logon modos adicionais não listados acima.</span><span class="sxs-lookup"><span data-stu-id="06cf9-142">Applications you have custom developed through hello [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="06cf9-143">Estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="06cf9-143">These include:</span></span>

-   <span data-ttu-id="06cf9-144">Logon baseado em [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code)</span><span class="sxs-lookup"><span data-stu-id="06cf9-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="06cf9-145">Logon baseado em [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code)</span><span class="sxs-lookup"><span data-stu-id="06cf9-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="06cf9-146">Logon baseado em [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html)</span><span class="sxs-lookup"><span data-stu-id="06cf9-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="06cf9-147">Logon baseado em [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference)</span><span class="sxs-lookup"><span data-stu-id="06cf9-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="06cf9-148">Saudação de leitura [guia do desenvolvedor do Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn mais informações sobre como o aplicativo toocreate um personalizado que dá suporte a esses único modos de logon.</span><span class="sxs-lookup"><span data-stu-id="06cf9-148">Read hello [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn more about how toocreate a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-tooset-an-applications-single-sign-on-mode"></a><span data-ttu-id="06cf9-149">Como um aplicativo de tooset do único modo de logon</span><span class="sxs-lookup"><span data-stu-id="06cf9-149">How tooset an application’s single sign-on mode</span></span>

<span data-ttu-id="06cf9-150">tooset um aplicativo **o logon único** modo, siga Olá instruções abaixo:</span><span class="sxs-lookup"><span data-stu-id="06cf9-150">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="06cf9-151">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="06cf9-151">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="06cf9-152">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="06cf9-152">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="06cf9-153">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="06cf9-153">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="06cf9-154">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="06cf9-154">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="06cf9-155">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="06cf9-155">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="06cf9-156">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="06cf9-156">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="06cf9-157">Selecione aplicativo hello para o qual você deseja tooconfigure-logon único.</span><span class="sxs-lookup"><span data-stu-id="06cf9-157">Select hello application for which you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="06cf9-158">Depois que o aplicativo hello carrega, clique em **o logon único** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="06cf9-158">Once hello application loads, click **Single sign-on** from hello application’s left hand navigation menu.</span></span>

## <a name="how-toochoose-a-provisioning-mode"></a><span data-ttu-id="06cf9-159">Como toochoose um modo de provisionamento</span><span class="sxs-lookup"><span data-stu-id="06cf9-159">How toochoose a provisioning mode</span></span>

-   <span data-ttu-id="06cf9-160">**Provisionamento manual** – escolha Olá [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) modo de provisionamento se você tem contas existentes ou deseja toomanage contas para este aplicativo fora do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06cf9-160">**Manual Provisioning** – choose hello [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish toomanage accounts for this application outside of Azure AD.</span></span>

-   <span data-ttu-id="06cf9-161">**O provisionamento automático** – escolha Olá [automático](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **modo de provisionamento** se você quiser tooenable baseada em API o provisionamento automático e/ou cancelamento de provisionamento de contas de usuário toothis aplicativo</span><span class="sxs-lookup"><span data-stu-id="06cf9-161">**Automatic Provisioning** – choose hello [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want tooenable automatic API-based provisioning and/or de-provisioning of user accounts toothis application</span></span> 

   >[!NOTE]
   ><span data-ttu-id="06cf9-162">Essa opção só está disponível para aplicativos em Olá **em destaque** categoria de saudação [Galeria de aplicativos do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="06cf9-162">This option is available only for applications within hello **featured** category of hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span></span>
   >
   >

-   <span data-ttu-id="06cf9-163">**Provisionamento automático baseado em SCIM** – use [provisionamento automático baseado em SCIM](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) se o seu aplicativo oferece suporte ao protocolo SCIM Olá para detectar alterações toousers e grupos, que são emitidos automaticamente para as alterações tooany aplicativo integrado ao AD do Azure</span><span class="sxs-lookup"><span data-stu-id="06cf9-163">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports hello SCIM protocol for detecting changes toousers and groups, which are automatically emitted for changes tooany application integrated with Azure AD</span></span> 

   >[!NOTE]
   ><span data-ttu-id="06cf9-164">Essa opção não está listada como um modo de provisionamento específico, mas está habilitada por padrão para todos os aplicativos integradas ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06cf9-164">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span></span>
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a><span data-ttu-id="06cf9-165">Como tooset um aplicativo do modo de provisionamento</span><span class="sxs-lookup"><span data-stu-id="06cf9-165">How tooset an application’s provisioning mode</span></span>

<span data-ttu-id="06cf9-166">tooset um aplicativo **provisionamento** modo, siga Olá instruções abaixo:</span><span class="sxs-lookup"><span data-stu-id="06cf9-166">tooset an application’s **provisioning** mode, follow hello instructions below:</span></span>

<span data-ttu-id="06cf9-167">tooset um aplicativo **o logon único** modo, siga Olá instruções abaixo:</span><span class="sxs-lookup"><span data-stu-id="06cf9-167">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="06cf9-168">Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="06cf9-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="06cf9-169">Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.</span><span class="sxs-lookup"><span data-stu-id="06cf9-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="06cf9-170">Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.</span><span class="sxs-lookup"><span data-stu-id="06cf9-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="06cf9-171">Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.</span><span class="sxs-lookup"><span data-stu-id="06cf9-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="06cf9-172">Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="06cf9-172">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="06cf9-173">Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="06cf9-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="06cf9-174">Selecione o aplicativo hello para o qual você deseja tooconfigure provisionamento.</span><span class="sxs-lookup"><span data-stu-id="06cf9-174">Select hello application for which you want tooconfigure provisioning.</span></span>

7.  <span data-ttu-id="06cf9-175">Depois que o aplicativo hello carrega, clique em **provisionamento** no menu de navegação à esquerda do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="06cf9-175">Once hello application loads, click **Provisioning** from hello application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06cf9-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="06cf9-176">Next steps</span></span>
[<span data-ttu-id="06cf9-177">Gerenciando aplicativos com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="06cf9-177">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
