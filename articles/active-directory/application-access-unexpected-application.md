---
title: aplicativo de aaaUnexpected na minha lista de aplicativos | Microsoft Docs
description: "Como toosee todos os aplicativos em seu locatário e entender como os aplicativos aparecem na sua lista de todos os aplicativos em aplicativos corporativos"
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
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a>Aplicativo inesperado em minha lista de aplicativos

Este artigo ajuda toounderstand como os aplicativos são exibidos em seu **todos os aplicativos** lista sob **aplicativos empresariais**. 

## <a name="how-toosee-all-applications-in-your-tenant"></a>Como toosee todos os aplicativos em seu locatário

toosee Olá a todos os aplicativos em seu locatário, é necessário Olá toouse **filtro** controlar tooshow **todos os aplicativos** em Olá **todos os aplicativos** lista. toodo isso, execute Olá estas etapas abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

6.  Clique em Olá use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos**.

7.  Em Olá **filtro** folha, Olá conjunto **Mostrar** opção muito**todos os aplicativos.**

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a>Por que um aplicativo específico aparece em minha lista de todos os aplicativos?

Quando filtrada muito**todos os aplicativos**, Olá **todos os aplicativos** **lista** mostra todos os objetos de entidade de serviço no seu locatário. Objetos de Entidade de Serviço podem aparecer nessa lista de uma várias maneiras:

1.  Quando você adicionar qualquer aplicativo da Galeria de aplicativo hello, incluindo:

   1. **Aplicativos da Galeria do Azure AD** – um aplicativo que foi integrado previamente para logon único com o Azure AD.

   2. **Aplicativos de Proxy de aplicativo** – um aplicativo em execução no seu ambiente local que você deseja tooprovide segura de logon único tooexternally.

   3. **Aplicativos personalizado** – Olá de um aplicativo que sua organização deseja toodevelop na plataforma de desenvolvimento de aplicativo do Azure AD, mas que talvez ainda não existir.

   4. **Aplicativos inexistentes na Galeria** – traga seus aplicativos! Qualquer link da web que você deseja, qualquer aplicativo que processa um campo de nome de usuário e senha, oferece suporte a protocolos SAML ou OpenID Connect ou oferece suporte a SCIM que você deseja toointegrate para logon único com o Azure AD.

2.  Ao se inscrever ou entrar em um aplicativo de <sup>terceiros</sup> integrado ao Azure Active Directory. Um exemplo disso é o [Smartsheet](https://app.smartsheet.com/b/home) ou o [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).

3.  Quando se inscrever ou adicionar um usuário de tooa de licença ou um grupo tooa primeiro aplicativo, como [Microsoft Office 365](http://products.office.com/).

4.  Quando você adiciona um novo registro de aplicativo, criando um aplicativo personalizado usando Olá [registro de aplicativos](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).

5.  Quando você adiciona um novo registro de aplicativo, criando um aplicativo personalizado usando Olá [Portal de registro de aplicativo v 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).

6.  Quando você adiciona um aplicativo que está desenvolvendo usando os [Métodos de autenticação do ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) ou os [Serviços Conectados](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx) do Visual Studio.

7.  Quando você cria um objeto de entidade de serviço usando Olá [módulo PowerShell do AD do Azure](/powershell/azure/install-adv2?view=azureadps-2.0).

8.  Quando você [consentimento de aplicativo tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) como dados de toouse um administrador no seu locatário.

9.  Quando um [tooan aplicativo consentimento do usuário](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse dados em seu locatário.

10. Quando você habilita determinados serviços que armazenam dados em seu locatário. Um exemplo disso é a redefinição de senha, que é modelada como um toostore principal do serviço sua senha redefinida política com segurança.

tooget obter mais detalhes sobre como os aplicativos são adicionados tooyour diretório, leia [como e por que os aplicativos são adicionados tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>Desejo tooremove aplicativos de tooan de atribuição de um usuário específico ou do grupo

tooremove um usuário ou grupo atribuição tooan aplicativo, execute as etapas de saudação listadas no hello [remover uma atribuição de usuário ou grupo de um aplicativo de empresa no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) artigo.

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a>Desejo toodisable todos os aplicativos de tooan de acesso para cada usuário

toodisable todos os usuário entradas tooan de aplicativos, siga etapas de saudação listadas Olá [desabilitar entradas do usuário para um aplicativo de empresa no Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) artigo.

## <a name="i-want-toodelete-an-application-entirely"></a>Desejo toodelete um aplicativo totalmente

muito**excluir um aplicativo**, siga as instruções de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global** ou **Co-administrador.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **aplicativos empresariais** no menu de navegação do hello Azure Active Directory à esquerda.

5.  Clique em **todos os aplicativos** tooview uma lista de todos os seus aplicativos.

  * Se você não vir o aplicativo hello você deseja mostrar aqui, use Olá **filtro** controle na parte superior de saudação do hello **lista de todos os aplicativos** e conjunto hello **Mostrar** opção muito **Todos os aplicativos.**

6.  Selecione o aplicativo hello deseja toodelete.

7.  Depois que o aplicativo hello carrega, clique em **excluir** ícone do aplicativo de superior hello **visão geral** folha.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>Desejo toodisable todos os aplicativos do usuário futuras consentimento operações tooany

Desabilitando o consentimento do usuário para seu diretório de todo a impedir que usuários finais de consentimento tooany aplicativo. Os administradores ainda podem consentir em nome dos usuários. toolearn mais sobre o aplicativo de consentimento e por que você pode ou não poderá toodo, leitura [usuário conhecimento e consentimento do administrador](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

muito**desabilitar todas as operações de consentimento do usuário futuras em seu diretório inteiro**, siga as instruções de saudação abaixo:

1.  Olá abrir [ **Portal do Azure** ](https://portal.azure.com/) e entre como um **Administrador Global.**

2.  Olá abrir **extensão do Active Directory do Azure** clicando **mais serviços** na parte inferior de saudação do menu de navegação esquerda principal hello.

3.  Digite **"Active Directory do Azure**" na caixa de pesquisa do filtro de hello e selecione Olá **Active Directory do Azure** item.

4.  Clique em **usuários e grupos** no menu de navegação hello.

5.  Clique em **Configurações de usuário**.

6.  Desabilitar todas as operações de consentimento do usuário futuro por configuração Olá **usuários podem permitir que aplicativos tooaccess seus dados** alternar muito**não** e clique em Olá **salvar** botão.

## <a name="next-steps"></a>Próximas etapas
[Gerenciando aplicativos com o Azure Active Directory](active-directory-enable-sso-scenario.md)
