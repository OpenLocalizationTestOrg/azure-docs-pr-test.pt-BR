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
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a>Desenvolver aplicativos de linha de negócios para o Azure Active Directory
Este guia fornece uma visão geral do desenvolvimento de aplicativos do linha de negócios (LoB) para o Azure AD (Active Directory) .hello deve público é que os administradores globais do Active Directory/Office 365.

## <a name="overview"></a>Visão geral
A criação de aplicativos integrados ao AD do Azure oferece aos usuários em sua organização logon único com o Office 365. Com o aplicativo hello no AD do Azure lhe dá que controle sobre a política de autenticação Olá para o aplicativo hello. toolearn mais sobre acesso condicional e como aplicativos de tooprotect com autenticação multifator (MFA), consulte [Configurando regras de acesso](active-directory-conditional-access-azuread-connected-apps.md).

Registre seu toouse de aplicativo do Active Directory do Azure. Registrar o aplicativo hello significa que os desenvolvedores podem usar usuários do AD do Azure tooauthenticate e solicitar acesso toouser recursos como email, calendário e documentos.

Qualquer membro do diretório (não convidados) pode registrar um aplicativo, também conhecido como *criação de um objeto de aplicativo*.

Registrar um aplicativo permite que qualquer usuário toodo Olá das seguintes:

* Obter uma identidade para o aplicativo que reconhece o AD do Azure
* Obtenha uma ou mais segredos/chaves que Olá aplicativo pode usar tooauthenticate próprio tooAD
* Aplicativo de hello marca no hello portal do Azure com um nome personalizado, logotipo, etc.
* Aplicar o aplicativo de tootheir de recursos de autorização do AD do Azure, incluindo:

  * RBAC (Controle de Acesso Baseado em Função)
  * Azure Active Directory como servidor de autorização do oAuth (proteger uma API exposta pelo aplicativo hello)
* Declare permissões exigidas necessárias para toofunction de aplicativo hello conforme o esperado, incluindo:

      - Permissões de aplicativo (somente administradores globais). Por exemplo: associação de função no outro AD do Azure aplicativo ou função de associação relativo tooan Azure recursos, grupo de recursos, ou a assinatura
      - Permissões (qualquer usuário). Por exemplo: Azure AD, Entrar e Ler o Perfil

> [!NOTE]
> Por padrão, qualquer membro pode registrar um aplicativo. toolearn como toorestrict permissões para registrar os membros de toospecific de aplicativos, consulte [como os aplicativos são adicionados tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).
>
>

Aqui está o que você, administrador global hello, precisam toodo toohelp desenvolvedores tornar seu aplicativo pronto para produção:

* Configurar regras de acesso (política de acesso/MFA)
* Configurar aplicativo hello de toorequire atribuição de usuário e atribuir usuários
* Suprimir a experiência de consentimento do usuário saudação padrão

## <a name="configure-access-rules"></a>Configurar regras de acesso
Configure aplicativos de SaaS de tooyour de regras de acesso por aplicativo. Por exemplo, você pode exigir a MFA ou permitir apenas acesso toousers em redes confiáveis. detalhes de saudação para este estão disponíveis no documento hello [Configurando regras de acesso](active-directory-conditional-access-azuread-connected-apps.md).

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a>Configurar aplicativo hello de toorequire atribuição de usuário e atribuir usuários
Por padrão, os usuários podem acessar aplicativos sem ser atribuídos. No entanto, se o aplicativo hello expõe funções ou se você quiser que o hello tooappear de aplicativo no painel de acesso do usuário, você deve exigir a atribuição do usuário.

[Exigindo atribuição do usuário](active-directory-applications-guiding-developers-requiring-user-assignment.md)

Caso você seja um assinante do Azure AD Premium ou EMS (Enterprise Mobility Suite), é altamente recomendável usar grupos. Atribuir grupos toohello aplicativo permite que você toodelegate acesso contínuo gerenciamento toohello proprietário do grupo de saudação. Você pode criar um grupo de saudação ou fazer parte responsável Olá em sua organização toocreate Olá grupo usando o recurso de gerenciamento de grupo.

[Atribuir usuários tooan aplicativo](active-directory-applications-guiding-developers-assigning-users.md)  
[Atribuir grupos de aplicativo tooan](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a>Suprimir o consentimento do usuário
Por padrão, cada usuário passa por um toosign de experiência de consentimento no. experiência de consentimento Hello, solicitando permissões a usuários toogrant tooan aplicativo, pode ser desconcertante para usuários que não estão familiarizados com essas decisões.

Para aplicativos que você confia, você pode simplificar a experiência do usuário de saudação pelo aplicativo de toohello consentimento em nome de sua organização.

Para obter mais informações sobre o consentimento do usuário e o consentimento de saudação experiência no Azure, consulte [integrando aplicativos com o Active Directory do Azure](active-directory-integrating-applications.md).

## <a name="related-articles"></a>Artigos relacionados
* [Habilitar acesso remoto seguro local tooon aplicativos com Proxy de aplicativo do Azure AD](active-directory-application-proxy-get-started.md)
* [Visualização de acesso condicional do Azure para aplicativos SaaS](active-directory-conditional-access-azuread-connected-apps.md)
* [Gerenciando acesso tooapps com o Azure AD](active-directory-managing-access-to-apps.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
