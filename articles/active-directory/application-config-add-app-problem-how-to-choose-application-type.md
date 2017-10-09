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
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a>Como toochoose qual aplicativo digite toouse ao adicionar um aplicativo

Este artigo ajuda toounderstand Olá quatro tipos principais de aplicativos, você pode integrar com o Azure AD:

* O que tem suporte em cada um deles
* Por que você escolheria cada aplicativo
* Como tooconfigure propriedades de núcleo do aplicativo desses, como usuários **provisionado**, ou o que **o logon único** toouse de tecnologia.

## <a name="supported-application-types-in-azure-ad"></a>Tipos de aplicativos com suporte no Azure AD

Olá do Azure AD oferece suporte a quatro principais tipos de aplicativos que você pode adicionar usando **adicionar** recurso encontrado em **aplicativos empresariais**. Estão incluídos:

-   **Aplicativos da Galeria do Azure AD** – um aplicativo que foi integrado previamente para logon único com o Azure AD.

-   **Aplicativos de Proxy de aplicativo** – um aplicativo em execução no seu ambiente local que você deseja tooprovide segura de logon único tooexternally.

-   **Aplicativos personalizado** – Olá de um aplicativo que sua organização deseja toodevelop na plataforma de desenvolvimento de aplicativo do Azure AD, mas que talvez ainda não existir.

-   **Aplicativos inexistentes na Galeria** – traga seus aplicativos! Qualquer link da web que você deseja, qualquer aplicativo que processa um campo de nome de usuário e senha, oferece suporte a protocolos SAML ou OpenID Connect ou oferece suporte a SCIM que você deseja toointegrate para logon único com o Azure AD.

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a>Recursos e recursos com suporte de todos os Olá acima tipos de aplicativos

Olá recursos a seguir têm suporte por qualquer Olá acima 4 tipos de aplicativo no AD do Azure:

-   **Início rápido** – familiarize-se rapidamente com um aplicativo executando [etapas simples de implantação](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)

-   **Gerenciamento de propriedades gerais** – obter um [deeplink direto](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) tooan aplicativo, [personalizar identidade visual Olá](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) de um aplicativo, ou [desativar aplicativo hello](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) para todos os usuários.

-   **Gerenciamento de usuário e grupo** – [atribuir](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) ou [remover](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) aplicativo tooan de usuários e grupos e, opcionalmente, atribua funções de aplicativo específicas de saudação esses usuários e grupos têm acesso ao

-   **Acesso de aplicativo de autoatendimento** – habilitar seu usuários toorequest [acesso de aplicativo de autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooan aplicativo de seu aplicativo acesso painéis adicionando um aplicativo diretamente ou [ ingressando em um grupo habilitado autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), opcionalmente, exigir a aprovação de negócios ao longo de saudação maneira

-   **Logs de logon** – consulte [todos Olá aplicativo de tooan entradas](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), ou todos os seus aplicativos

-   **Logs de auditoria** – consulte [logs de auditoria sobre o aplicativo de tooan modificações detalhados](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), ou tooall seus aplicativos

-   **Acesso condicional baseado em risco e** – defina poderosa [regras de acesso com base em condição](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) que são aplicadas quando os usuários tentam toosign no aplicativo específico tooa

-   **Permissões de exibição** – exibir qualquer Olá [OAuth2 permissões](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) um aplicativo tem acesso tooin seu diretório de um único local

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Modos de logon único e provisionamento com suporte de tipos específicos de aplicativos

Olá tabela a seguir descreve Olá diferentes logon único e provisionamento modos suportados por cada Olá acima tipos de aplicativos. Você pode usar essa tabela toohelp toounderstand qual aplicativo precisar tooadd toosupport uma meta específica.

  ![Tabela de tipos de aplicativo](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>Como toochoose um modo de logon único

Olá suportada **o logon único** modos para aplicativos do Azure AD estão listados abaixo.

-   **Azure AD SSO desabilitado** – escolha AD do Azure SSO desabilitado **modo de logon único** se você ainda não está pronto toointegrate este aplicativo com logon único com o Azure AD ou são simplesmente experimentá-lo

-   **Vinculado logon** – escolha Olá [logon vinculado](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modo de logon único** se você tiver um aplicativo que já está conectado com uma único logon solução existente, ou se você quiser apenas toopublish simples de link para os usuários em seus [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) ou [iniciador do aplicativo Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Com base em senha de logon** – escolha Olá [baseada em senha logon](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modo de logon único** se seu aplicativo processa um campo de nome de usuário e senha do HTML e você desejar toostore que nome de usuário e senha repetido de toobe com segurança toohello aplicativo mais tarde

-   **Baseado no SAML logon** – escolha Olá [baseado no SAML logon](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) toospecific funções de aplicativo de logon único no modo se seu aplicativo dá suporte a protocolos SAML ou OpenID Connect hello, ou toobe toomap capaz de usuários com base em regras que você definir no seu SAML declarações *

   >[!NOTE]
   >Essa opção não está disponível quando o proxy de aplicativo hello está configurado para um aplicativo.
   >
   >

-   **Com base no cabeçalho de logon** – Escolha esta opção [com base no cabeçalho de logon](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) autenticação que você deseja tooperform de logon único no muito baseada em único modo de logon se você tiver um aplicativo usando PingAccess que dá suporte ao cabeçalho HTTP

   >[!NOTE]
   >Essa opção só está disponível quando o proxy de aplicativo hello e PingAccess está configurado para um aplicativo.
   >
   >

-   **Autenticação integrada do Windows** – escolha Olá [autenticação integrada do Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) em modo ao expor um aplicativo WIA local que você deseja tooperform de logon único no muito do logon único

   >[!NOTE]
   >Essa opção só está disponível quando o proxy de aplicativo hello está configurado para um aplicativo.
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a>Modos de logon único para aplicativos personalizados

Aplicativos que você tiver personalizado desenvolvido por meio de saudação [aplicativo personalizado](#_Custom-Developed_Applications) experiência também oferece suporte para único logon modos adicionais não listados acima. Estão incluídos:

-   Logon baseado em [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code)

-   Logon baseado em [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code)

-   Logon baseado em [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html)

-   Logon baseado em [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference)

Saudação de leitura [guia do desenvolvedor do Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn mais informações sobre como o aplicativo toocreate um personalizado que dá suporte a esses único modos de logon.

## <a name="how-tooset-an-applications-single-sign-on-mode"></a>Como um aplicativo de tooset do único modo de logon

tooset um aplicativo **o logon único** modo, siga Olá instruções abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione aplicativo hello para o qual você deseja tooconfigure-logon único.

7.  Depois que o aplicativo hello carrega, clique em **o logon único** no menu de navegação à esquerda do aplicativo hello.

## <a name="how-toochoose-a-provisioning-mode"></a>Como toochoose um modo de provisionamento

-   **Provisionamento manual** – escolha Olá [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) modo de provisionamento se você tem contas existentes ou deseja toomanage contas para este aplicativo fora do Azure AD.

-   **O provisionamento automático** – escolha Olá [automático](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **modo de provisionamento** se você quiser tooenable baseada em API o provisionamento automático e/ou cancelamento de provisionamento de contas de usuário toothis aplicativo 

   >[!NOTE]
   >Essa opção só está disponível para aplicativos em Olá **em destaque** categoria de saudação [Galeria de aplicativos do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).
   >
   >

-   **Provisionamento automático baseado em SCIM** – use [provisionamento automático baseado em SCIM](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) se o seu aplicativo oferece suporte ao protocolo SCIM Olá para detectar alterações toousers e grupos, que são emitidos automaticamente para as alterações tooany aplicativo integrado ao AD do Azure 

   >[!NOTE]
   >Essa opção não está listada como um modo de provisionamento específico, mas está habilitada por padrão para todos os aplicativos integradas ao Azure AD.
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a>Como tooset um aplicativo do modo de provisionamento

tooset um aplicativo **provisionamento** modo, siga Olá instruções abaixo:

tooset um aplicativo **o logon único** modo, siga Olá instruções abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello para o qual você deseja tooconfigure provisionamento.

7.  Depois que o aplicativo hello carrega, clique em **provisionamento** no menu de navegação à esquerda do aplicativo hello.

## <a name="next-steps"></a>Próximas etapas
[Gerenciando aplicativos com o Azure Active Directory](active-directory-enable-sso-scenario.md)
