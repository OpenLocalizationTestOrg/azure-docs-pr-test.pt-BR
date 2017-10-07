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
# <a name="how-toodetermine-what-single-sign-on-method-toouse"></a>Como toodetermine o logon único no método toouse

Este artigo ajuda toounderstand Olá único logon modos suportados pelo AD do Azure e como toopick quais um toochoose para Olá aplicativo que lhe interessam.

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a>Modos de logon único e provisionamento com suporte de tipos específicos de aplicativos

Olá tabela a seguir descreve Olá diferentes logon único e provisionamento modos suportados por cada Olá acima tipos de aplicativos. Você pode usar essa tabela toohelp toounderstand qual aplicativo precisar tooadd toosupport uma meta específica.

  ![Tabela de tipos de aplicativo](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a>Como toochoose um modo de logon único

Olá suportada **o logon único** modos para aplicativos do Azure AD estão listados abaixo.

-   **Azure AD SSO desabilitado** – escolha AD do Azure SSO desabilitado **modo de logon único** se você ainda não está pronto toointegrate este aplicativo com logon único com o Azure AD ou são simplesmente experimentá-lo

-   **Vinculado logon** – escolha Olá [logon vinculado](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modo de logon único** se você tiver um aplicativo que já está conectado com uma único logon solução existente, ou se você quiser apenas toopublish simples de link para os usuários em seus [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) ou [iniciador do aplicativo Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)

-   **Com base em senha de logon** – escolha Olá [baseada em senha logon](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **modo de logon único** se seu aplicativo processa um campo de nome de usuário e senha do HTML e você desejar toostore que nome de usuário e senha repetido de toobe com segurança toohello aplicativo mais tarde

-   **Baseado no SAML logon** – escolha Olá [baseado no SAML logon](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) toospecific funções de aplicativo de logon único no modo se seu aplicativo dá suporte a protocolos SAML ou OpenID Connect hello, ou toobe toomap capaz de usuários com base em regras que você definir no seu SAML declarações *(**Observação:** essa opção não está disponível quando o proxy de aplicativo hello está configurado para um aplicativo) *

-   **Com base no cabeçalho de logon** – Escolha esta opção [com base no cabeçalho de logon](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) autenticação que você deseja tooperform de logon único no muito baseada em único modo de logon se você tiver um aplicativo usando PingAccess que dá suporte ao cabeçalho HTTP *(**Observação:** essa opção só está disponível quando o proxy de aplicativo hello e PingAccess está configurado para um aplicativo) *

-   **Autenticação integrada do Windows** – escolha Olá [autenticação integrada do Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) de logon único modo ao expor um aplicativo WIA local que você deseja tooperform de logon único no muito*(*  *Observação:** essa opção só está disponível quando o proxy de aplicativo hello está configurado para um aplicativo) *

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

6.  Selecionar aplicativo hello deseja tooconfigure-logon único

7.  Depois que o aplicativo hello carrega, clique em **o logon único** no menu de navegação à esquerda do aplicativo hello.

## <a name="next-steps"></a>Próximas etapas
[Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo](active-directory-application-proxy-sso-using-kcd.md)

