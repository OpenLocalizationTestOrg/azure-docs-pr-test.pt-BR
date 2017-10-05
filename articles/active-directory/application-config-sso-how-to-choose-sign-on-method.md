---
title: "Como determinar o método de logon único a ser usado | Microsoft Docs"
description: "Compreenda os modos de logon único com suporte do Azure AD e como escolher qual deles deve ser usado para o aplicativo em que você está interessado."
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
ms.openlocfilehash: 80f4a965920fec9cb578c1bee235c7857f37431e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-determine-what-single-sign-on-method-to-use"></a><span data-ttu-id="6613c-103">Como determinar o método de logon único a ser usado</span><span class="sxs-lookup"><span data-stu-id="6613c-103">How to determine what single-sign on method to use</span></span>

<span data-ttu-id="6613c-104">Este artigo o ajuda a compreender os modos de logon único com suporte do Azure AD e como escolher qual deles deve ser usado para o aplicativo em que você está interessado.</span><span class="sxs-lookup"><span data-stu-id="6613c-104">This article help you to understand the single sign-on modes supported by Azure AD and how to pick which one to choose for the application you are interested in.</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="6613c-105">Modos de logon único e provisionamento com suporte de tipos específicos de aplicativos</span><span class="sxs-lookup"><span data-stu-id="6613c-105">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="6613c-106">A tabela a seguir descreve os diferente modos de logon único e provisionamento com suporte de cada um dos tipos de aplicativos mencionados acima.</span><span class="sxs-lookup"><span data-stu-id="6613c-106">The table below describes the different single sign-on and provisioning modes supported by each of the above application types.</span></span> <span data-ttu-id="6613c-107">Use essa tabela como um auxílio para entender qual aplicativo você precisa adicionar a fim de dar suporte a um objetivo específico.</span><span class="sxs-lookup"><span data-stu-id="6613c-107">You can use this table to help you to understand which application you need to add to support a specific goal.</span></span>

  ![Tabela de tipos de aplicativo](./media/application-tables/table1.png)

## <a name="how-to-choose-a-single-sign-on-mode"></a><span data-ttu-id="6613c-109">Como escolher um modo de logon único</span><span class="sxs-lookup"><span data-stu-id="6613c-109">How to choose a single sign-on mode</span></span>

<span data-ttu-id="6613c-110">Os modos de **logon único** com suporte para aplicativos do Azure AD estão listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="6613c-110">The supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="6613c-111">**Logon único do Azure AD desabilitado** – escolha o **modo de logon único** desabilitado do Azure AD se você ainda não estiver pronto para integrar esse aplicativo com logon único ao Azure AD ou se apenas o estiver testando</span><span class="sxs-lookup"><span data-stu-id="6613c-111">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="6613c-112">**Logon vinculado** – escolha o **modo de logon único** [Logon vinculado](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) se você tiver um aplicativo que já está conectado a uma solução de logon único existente, ou se quiser apenas publicar um link simples para seus usuários no [Painel de Acesso do Aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) ou no [Inicializador de aplicativos do Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="6613c-112">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="6613c-113">**Logon baseado em senha** – escolha o **modo de logon único** [Logon baseado em senha](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) se seu aplicativo renderizar um campo de nome de usuário e senha em HTML e você quiser armazenar esse nome de usuário e senha com segurança para reprodução no aplicativo mais tarde</span><span class="sxs-lookup"><span data-stu-id="6613c-113">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span></span>

-   <span data-ttu-id="6613c-114">**Logon baseado em SAML** – escolha o modo de logon único [Logon baseado em SAML](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) se seu aplicativo der suporte aos protocolos SAML ou OpenID Connect ou se você quiser mapear usuários a funções de aplicativo específicas com base em regras que você define em suas declarações SAML *(**Observação:** esta opção não fica disponível quando o proxy de aplicativo está configurado para um aplicativo)*</span><span class="sxs-lookup"><span data-stu-id="6613c-114">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims *(**Note:** this option is not available when the application proxy is configured for an application)*</span></span>

-   <span data-ttu-id="6613c-115">**Logon baseado em cabeçalho** – escolha o modo de logon único [Logon baseado em cabeçalho](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) se você tiver um aplicativo que usa PingAccess e que dá suporte à autenticação baseada em cabeçalho HTTP em que você deseja realizar logon único *(**Observação:** esta opção fica disponível somente quando o proxy de aplicativo e o PingAccess estão configurados para um aplicativo)*</span><span class="sxs-lookup"><span data-stu-id="6613c-115">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish to perform single-sign on to *(**Note:** this option is only available when the application proxy and PingAccess is configured for an application)*</span></span>

-   <span data-ttu-id="6613c-116">**Autenticação integrada do Windows** – escolha o modo de logon único [Autenticação integrada do Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) ao expor um aplicativo WIA local no qual você deseja realizar o logon único *(**Observação:** esta opção fica disponível apenas quando o proxy de aplicativo está configurado para um aplicativo)*</span><span class="sxs-lookup"><span data-stu-id="6613c-116">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to *(**Note:** this option is only available when the application proxy is configured for an application)*</span></span>

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="6613c-117">Modos de logon único para aplicativos personalizados</span><span class="sxs-lookup"><span data-stu-id="6613c-117">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="6613c-118">Aplicativos desenvolvidos de forma personalizada por meio da experiência [Aplicativo desenvolvido de forma personalizada](#_Custom-Developed_Applications) também dão suporte a modos de logon único adicionais não listados acima.</span><span class="sxs-lookup"><span data-stu-id="6613c-118">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="6613c-119">Estão incluídos:</span><span class="sxs-lookup"><span data-stu-id="6613c-119">These include:</span></span>

-   <span data-ttu-id="6613c-120">Logon baseado em [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code)</span><span class="sxs-lookup"><span data-stu-id="6613c-120">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="6613c-121">Logon baseado em [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code)</span><span class="sxs-lookup"><span data-stu-id="6613c-121">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="6613c-122">Logon baseado em [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html)</span><span class="sxs-lookup"><span data-stu-id="6613c-122">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="6613c-123">Logon baseado em [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference)</span><span class="sxs-lookup"><span data-stu-id="6613c-123">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="6613c-124">Leia o [Guia do Desenvolvedor do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) para saber mais sobre como criar um aplicativo desenvolvido de forma personalizada que dá suporte a esses modos de logon único.</span><span class="sxs-lookup"><span data-stu-id="6613c-124">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-to-set-an-applications-single-sign-on-mode"></a><span data-ttu-id="6613c-125">Como definir o modo de logon único de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="6613c-125">How to set an application’s single sign-on mode</span></span>

<span data-ttu-id="6613c-126">Para definir o modo de **logon único** de um aplicativo, siga as instruções abaixo:</span><span class="sxs-lookup"><span data-stu-id="6613c-126">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="6613c-127">Abra o [**Portal do Azure**](https://portal.azure.com/) e entre como **Administrador Global** ou **Coadministrador.**</span><span class="sxs-lookup"><span data-stu-id="6613c-127">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="6613c-128">Abra a **Extensão do Azure Active Directory** clicando em **Mais serviços** na parte inferior do menu de navegação esquerdo principal.</span><span class="sxs-lookup"><span data-stu-id="6613c-128">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="6613c-129">Digite **“Azure Active Directory**” na caixa de pesquisa do filtro e selecione o item **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6613c-129">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="6613c-130">Clique em **Aplicativos Empresariais** no menu de navegação esquerdo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6613c-130">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="6613c-131">Clique em **Todos os Aplicativos** para exibir uma lista com todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="6613c-131">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="6613c-132">Se não vir o aplicativo desejado, use o controle **Filtro** na parte superior da **Lista com Todos os Aplicativos** e defina a opção **Mostrar** como **Todos os Aplicativos.**</span><span class="sxs-lookup"><span data-stu-id="6613c-132">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="6613c-133">Selecione o aplicativo para o qual deseja configurar o logon único</span><span class="sxs-lookup"><span data-stu-id="6613c-133">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="6613c-134">Após o carregamento do aplicativo, clique em **Logon único** no menu de navegação esquerdo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6613c-134">Once the application loads, click **Single sign-on** from the application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6613c-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6613c-135">Next steps</span></span>
[<span data-ttu-id="6613c-136">Fornecer logon único para seus aplicativos com Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="6613c-136">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

