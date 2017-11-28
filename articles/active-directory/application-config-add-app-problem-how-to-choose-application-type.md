---
title: Como escolher o tipo de aplicativo a ser usado ao adicionar um aplicativo | Microsoft Docs
description: "Entenda os tipos de aplicativos com suporte que você pode integrar ao Azure AD e suas opções de configuração relacionadas"
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
ms.openlocfilehash: e0d41d1933531c2c633613bcbc1bbcbf075d6a69
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-choose-which-application-type-to-use-when-adding-an-application"></a><span data-ttu-id="5d9ac-103">Como escolher o tipo de aplicativo a ser usado ao adicionar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="5d9ac-103">How to choose which application type to use when adding an application</span></span>

<span data-ttu-id="5d9ac-104">Este artigo o ajuda você a entender os quatro tipos principais de aplicativos que você pode integrar ao Azure AD:</span><span class="sxs-lookup"><span data-stu-id="5d9ac-104">This article help you to understand the four main types of applications you can integrate with Azure AD:</span></span>

* <span data-ttu-id="5d9ac-105">O que tem suporte em cada um deles</span><span class="sxs-lookup"><span data-stu-id="5d9ac-105">What is supported by each of them</span></span>
* <span data-ttu-id="5d9ac-106">Por que você escolheria cada aplicativo</span><span class="sxs-lookup"><span data-stu-id="5d9ac-106">Why you might choose which application</span></span>
* <span data-ttu-id="5d9ac-107">Como configurar propriedades principais desses aplicativos, como quantos usuários são **provisionados** ou qual tecnologia de **logon único** usar.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-107">How to configure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology to use.</span></span>

## <a name="supported-application-types-in-azure-ad"></a><span data-ttu-id="5d9ac-108">Tipos de aplicativos com suporte no Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d9ac-108">Supported application types in Azure AD</span></span>

<span data-ttu-id="5d9ac-109">O Azure AD oferece suporte a quatro tipos de aplicativos principais que você pode adicionar usando o recurso **Adicionar** encontrado em **Aplicativos Empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-109">Azure AD supports four main application types that you can add using the **Add** feature found under **Enterprise Applications**.</span></span> <span data-ttu-id="5d9ac-110">Estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="5d9ac-110">These include:</span></span>

-   <span data-ttu-id="5d9ac-111">**Aplicativos da galeria do Azure AD** – Um aplicativo que foi previamente integrado para logon único com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

-   <span data-ttu-id="5d9ac-112">**Aplicativos do Proxy de Aplicativo** – um aplicativo em execução em seu ambiente local para o qual você deseja fornecer logon único seguro externamente.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-112">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

-   <span data-ttu-id="5d9ac-113">**Aplicativos desenvolvidos de forma personalizada** – um aplicativo que sua organização deseja desenvolver na Plataforma de Desenvolvimento de Aplicativos do Azure AD, mas que talvez ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-113">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

-   <span data-ttu-id="5d9ac-114">**Aplicativos inexistentes na Galeria** – traga seus aplicativos!</span><span class="sxs-lookup"><span data-stu-id="5d9ac-114">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="5d9ac-115">Qualquer link da Web desejado, ou qualquer aplicativo que processa um campo de nome de usuário e senha, dá suporte aos protocolos SAML ou OpenID Connect, ou dá suporte ao SCIM que você deseja integrar para logon único com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-115">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

## <a name="features-and-capabilities-supported-by-all-the-above-application-types"></a><span data-ttu-id="5d9ac-116">Recursos compatíveis com todos os tipos de aplicativo mencionados acima</span><span class="sxs-lookup"><span data-stu-id="5d9ac-116">Features and capabilities supported by all the above application types</span></span>

<span data-ttu-id="5d9ac-117">Os recursos a seguir têm suporte de qualquer um dos quatro tipos de aplicativos mencionados acima no Azure AD:</span><span class="sxs-lookup"><span data-stu-id="5d9ac-117">The following features are supported by any of the above 4 application types in Azure AD:</span></span>

-   <span data-ttu-id="5d9ac-118">**Início rápido** – familiarize-se rapidamente com um aplicativo executando [etapas simples de implantação](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span><span class="sxs-lookup"><span data-stu-id="5d9ac-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span></span>

-   <span data-ttu-id="5d9ac-119">**Gerenciamento de propriedades gerais** – obtenha um [deeplink direto](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) para um aplicativo, [personalize a marca](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) de um aplicativo ou [desabilite o aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) para todos os usuários.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) to an application, [customize the branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable the application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span></span>

-   <span data-ttu-id="5d9ac-120">**Gerenciamento de usuário e grupo** – [atribua](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) ou [remova](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) usuários e grupos de um aplicativo e, como opção, atribua as funções específicas de aplicativo as quais esses usuários e grupos têm acesso</span><span class="sxs-lookup"><span data-stu-id="5d9ac-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups to an application, and optionally assign the specific application roles these users and groups have access to</span></span>

-   <span data-ttu-id="5d9ac-121">**Acesso de autoatendimento ao aplicativo** – permita que os usuários solicitem o [acesso de autoatendimento ao aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) de seus Painéis de acesso do aplicativo por meio da adição direta de um aplicativo ou [ingressando em um grupo habilitado para autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), podendo exigir a aprovação comercial durante o processo</span><span class="sxs-lookup"><span data-stu-id="5d9ac-121">**Self-service application access** – enable your users to request [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to an application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along the way</span></span>

-   <span data-ttu-id="5d9ac-122">**Logs de entrada** – confira [todas as entradas em um aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), ou em todos os seus aplicativos</span><span class="sxs-lookup"><span data-stu-id="5d9ac-122">**Sign-in logs** – see [all the sign-ins to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span></span>

-   <span data-ttu-id="5d9ac-123">**Logs de auditoria** – confira [logs detalhados de auditoria sobre modificações feitas em um aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), ou em todos os seus aplicativos</span><span class="sxs-lookup"><span data-stu-id="5d9ac-123">**Audit logs** – see [detailed audit logs about modifications to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or to all your applications</span></span>

-   <span data-ttu-id="5d9ac-124">**Acesso condicional e com base em risco** – defina [regras avançadas de acesso com base em condição](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) que são aplicadas quando os usuários tentam entrar em um aplicativo específico</span><span class="sxs-lookup"><span data-stu-id="5d9ac-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt to sign in to a specific application</span></span>

-   <span data-ttu-id="5d9ac-125">**Exibição de permissões** – veja qualquer uma das [permissões de OAuth2](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) as quais um aplicativo tem acesso em seu diretório de um único local</span><span class="sxs-lookup"><span data-stu-id="5d9ac-125">**Permissions view** – view any of the [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access to in your directory from a single place</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="5d9ac-126">Modos de logon único e provisionamento com suporte de tipos específicos de aplicativos</span><span class="sxs-lookup"><span data-stu-id="5d9ac-126">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="5d9ac-127">A tabela a seguir descreve os diferente modos de logon único e provisionamento com suporte de cada um dos tipos de aplicativos mencionados acima.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-127">The table below describes the different single sign-on and provisioning modes supported by each of the above application types.</span></span> <span data-ttu-id="5d9ac-128">Use essa tabela como uma ajuda para entender quais aplicativos você precisa adicionar a fim de dar suporte a um objetivo específico.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-128">You can use this table to help you to understand which application you need to add to support a specific goal.</span></span>

  ![Tabela de tipos de aplicativo](./media/application-tables/table1.png)

## <a name="how-to-choose-a-single-sign-on-mode"></a><span data-ttu-id="5d9ac-130">Como escolher um modo de logon único</span><span class="sxs-lookup"><span data-stu-id="5d9ac-130">How to choose a single sign-on mode</span></span>

<span data-ttu-id="5d9ac-131">Os modos de **logon único** com suporte para aplicativos do Azure AD estão listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-131">The supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="5d9ac-132">**Logon único do Azure AD desabilitado** – escolha o **modo de logon único** desabilitado do Azure AD se você ainda não estiver pronto para integrar esse aplicativo com logon único ao Azure AD ou se apenas o estiver testando</span><span class="sxs-lookup"><span data-stu-id="5d9ac-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="5d9ac-133">**Logon vinculado** – escolha o **modo de logon único** [Logon vinculado](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) se você tiver um aplicativo que já está conectado a uma solução de logon único existente, ou se quiser apenas publicar um link simples para seus usuários no [Painel de Acesso do Aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) ou no [Inicializador de aplicativos do Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="5d9ac-133">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="5d9ac-134">**Logon baseado em senha** – Escolha o **modo de logon único** [Logon baseado em senha](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) se seu aplicativo renderizar um campo de nome de usuário e senha em HTML e você quiser armazenar esse nome de usuário e senha com segurança para reprodução no aplicativo mais tarde</span><span class="sxs-lookup"><span data-stu-id="5d9ac-134">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span></span>

-   <span data-ttu-id="5d9ac-135">**Logon baseado em SAML** – Escolha o modo de logon único [Logon baseado em SAML](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) se o seu aplicativo der suporte aos protocolos SAML ou OpenID Connect, ou se você quiser mapear usuários a funções de aplicativo específicas com base em regras que você define em suas declarações SAML *</span><span class="sxs-lookup"><span data-stu-id="5d9ac-135">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims *</span></span>

   >[!NOTE]
   ><span data-ttu-id="5d9ac-136">Essa opção não está disponível quando o proxy de aplicativo está configurado para um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-136">This option is not available when the application proxy is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="5d9ac-137">**logon baseado em cabeçalho** – Escolha este modo de logon único [Logon baseado em cabeçalho](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) se você tiver um aplicativo usando PingAccess que oferece suporte à autenticação baseada em cabeçalho HTTP no qual deseja realizar logon único</span><span class="sxs-lookup"><span data-stu-id="5d9ac-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="5d9ac-138">Essa opção está disponível apenas quando o proxy de aplicativo e o PingAccess estiverem configurados para um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-138">This option is only available when the application proxy and PingAccess is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="5d9ac-139">**Autenticação integrada do Windows** – Escolha o modo de logon único [Autenticação integrada do Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) ao expor um aplicativo WIA local no qual você deseja realizar o logon único</span><span class="sxs-lookup"><span data-stu-id="5d9ac-139">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="5d9ac-140">Essa opção só está disponível quando o proxy de aplicativo estiver configurado para um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-140">This option is only available when the application proxy is configured for an application.</span></span>
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="5d9ac-141">Modos de logon únicos para aplicativos desenvolvidos de forma personalizada</span><span class="sxs-lookup"><span data-stu-id="5d9ac-141">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="5d9ac-142">Aplicativos desenvolvidos de forma personalizada por meio da experiência [Aplicativo desenvolvido de forma personalizada](#_Custom-Developed_Applications) também dão suporte a modos de logon único adicionais não listados acima.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-142">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="5d9ac-143">Estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="5d9ac-143">These include:</span></span>

-   <span data-ttu-id="5d9ac-144">Logon baseado em [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code)</span><span class="sxs-lookup"><span data-stu-id="5d9ac-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="5d9ac-145">Logon baseado em [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code)</span><span class="sxs-lookup"><span data-stu-id="5d9ac-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="5d9ac-146">Logon baseado em [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html)</span><span class="sxs-lookup"><span data-stu-id="5d9ac-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="5d9ac-147">Logon baseado em [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference)</span><span class="sxs-lookup"><span data-stu-id="5d9ac-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="5d9ac-148">Leia o [Guia do Desenvolvedor do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) para saber mais sobre como criar um aplicativo desenvolvido de forma personalizada que dá suporte a esses modos de logon único.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-148">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-to-set-an-applications-single-sign-on-mode"></a><span data-ttu-id="5d9ac-149">Como definir o modo de logon único de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="5d9ac-149">How to set an application’s single sign-on mode</span></span>

<span data-ttu-id="5d9ac-150">Para definir o modo de **logon único** de um aplicativo, siga as instruções abaixo:</span><span class="sxs-lookup"><span data-stu-id="5d9ac-150">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="5d9ac-151">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="5d9ac-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5d9ac-152">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5d9ac-153">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5d9ac-154">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5d9ac-155">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-155">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5d9ac-156">Se você não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="5d9ac-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5d9ac-157">Selecione o aplicativo para o qual você deseja configurar o logon único.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-157">Select the application for which you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="5d9ac-158">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-158">Once the application loads, click **Single sign-on** from the application’s left hand navigation menu.</span></span>

## <a name="how-to-choose-a-provisioning-mode"></a><span data-ttu-id="5d9ac-159">Como escolher um modo de provisionamento</span><span class="sxs-lookup"><span data-stu-id="5d9ac-159">How to choose a provisioning mode</span></span>

-   <span data-ttu-id="5d9ac-160">**Provisionamento Manual** – Escolha o modo de provisionamento [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) se você tiver contas ou se quiser gerenciar as contas desse aplicativo fora do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-160">**Manual Provisioning** – choose the [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish to manage accounts for this application outside of Azure AD.</span></span>

-   <span data-ttu-id="5d9ac-161">**Provisionamento Automático** – Escolha o **modo de provisionamento** [Automático](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) se você quiser habilitar o provisionamento automático baseado em API e/ou o desprovisionamento de contas de usuário para esse aplicativo</span><span class="sxs-lookup"><span data-stu-id="5d9ac-161">**Automatic Provisioning** – choose the [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want to enable automatic API-based provisioning and/or de-provisioning of user accounts to this application</span></span> 

   >[!NOTE]
   ><span data-ttu-id="5d9ac-162">Essa opção está disponível somente para aplicativos dentro da categoria **em destaque** da [Galeria de Aplicativos do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="5d9ac-162">This option is available only for applications within the **featured** category of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span></span>
   >
   >

-   <span data-ttu-id="5d9ac-163">**Provisionamento Automático baseado em SCIM** – Use o [Provisionamento Automático baseado em SCIM](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) se o seu aplicativo der suporte ao protocolo SCIM para detecção de alterações em usuários e grupos, que são emitidas automaticamente para alterações em qualquer aplicativo integrado ao Azure AD</span><span class="sxs-lookup"><span data-stu-id="5d9ac-163">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports the SCIM protocol for detecting changes to users and groups, which are automatically emitted for changes to any application integrated with Azure AD</span></span> 

   >[!NOTE]
   ><span data-ttu-id="5d9ac-164">Essa opção não está listada como um modo de provisionamento específico, mas está habilitada por padrão para todos os aplicativos integradas ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-164">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span></span>
   >
   >

## <a name="how-to-set-an-applications-provisioning-mode"></a><span data-ttu-id="5d9ac-165">Como configurar o modo de provisionamento de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="5d9ac-165">How to set an application’s provisioning mode</span></span>

<span data-ttu-id="5d9ac-166">Para definir o modo de **provisionando** de um aplicativo, siga as instruções abaixo:</span><span class="sxs-lookup"><span data-stu-id="5d9ac-166">To set an application’s **provisioning** mode, follow the instructions below:</span></span>

<span data-ttu-id="5d9ac-167">Para definir o modo de **logon único** de um aplicativo, siga as instruções abaixo:</span><span class="sxs-lookup"><span data-stu-id="5d9ac-167">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="5d9ac-168">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="5d9ac-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="5d9ac-169">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5d9ac-170">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5d9ac-171">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="5d9ac-172">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-172">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="5d9ac-173">Se você não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="5d9ac-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="5d9ac-174">Selecione o aplicativo para o qual você deseja configurar o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-174">Select the application for which you want to configure provisioning.</span></span>

7.  <span data-ttu-id="5d9ac-175">Após o carregamento do aplicativo, clique em **Provisionamento** no menu de navegação à esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5d9ac-175">Once the application loads, click **Provisioning** from the application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d9ac-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5d9ac-176">Next steps</span></span>
[<span data-ttu-id="5d9ac-177">Gerenciando aplicativos com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d9ac-177">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
