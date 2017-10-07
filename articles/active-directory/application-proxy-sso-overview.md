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
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a>Como o Proxy de Aplicativo do Azure AD fornece logon único?

O logon único é um elemento fundamental do Proxy de Aplicativo Azure AD.  Ele fornece a melhor experiência de usuário Olá porque os usuários têm apenas toosign em tooAzure do Active Directory na nuvem hello. Depois que eles autenticam tooAzure do Active Directory, o conector de Proxy de aplicativo hello manipula aplicativo local do hello autenticação toohello. aplicativo de back-end Hello não pode determinar a diferença de saudação entre um usuário remoto entrar por meio do Proxy de aplicativo e um uso comum em um dispositivo ingressado no domínio. 

toouse Active Directory do Azure para aplicativos tooyour de logon único, você precisa tooselect **Active Directory do Azure** como método de pré-autenticação hello. Se você selecionar **passagem** , em seguida, os usuários não autenticar tooAzure do Active Directory em todos os, mas são direcionados toohello simples aplicativo. Você pode configurar essa configuração quando você publica um aplicativo, ou navegue tooyour aplicativo hello portal do Azure e editar as configurações de Proxy de aplicativo hello. 

toosee seu único opções de logon, siga estas etapas:

1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Navegue muito**Active Directory do Azure** > **aplicativos empresariais** > **todos os aplicativos**.
3. Olá selecione aplicativo cujo logon único opções você deseja toomanage.
4. Selecione **Logon único**.

   ![Menu suspenso de logon único](./media/application-proxy-sso-overview/single-sign-on-mode.png)

menu suspenso de saudação mostra cinco opções para o aplicativo tooyour de logon único:

* Logon único do Azure AD desabilitado
* Logon baseado em senha
* Logon vinculado
* Autenticação Integrada do Windows
* Logon baseado em cabeçalho

## <a name="azure-ad-single-sign-on-disabled"></a>Logon único do Azure AD desabilitado

Se você não quiser a integração do Active Directory do Azure toouse tooyour de logon único aplicativo, escolha **AD do Azure SSO desabilitado**. Com essa opção selecionada, os usuários podem ter de se autenticar duas vezes. Primeiro, eles autenticar tooAzure do Active Directory e, em seguida, entre no próprio aplicativo toohello. 

Essa opção é uma boa opção se seu aplicativo local não precisa tooauthenticate de usuários, mas você deseja tooadd Active Directory do Azure como uma camada de segurança de acesso remoto. 

## <a name="password-based-sign-on"></a>Logon baseado em senha

Se você quiser toouse Active Directory do Azure como um cofre de senhas para os aplicativos no local, escolha **baseada em senha logon**. Essa opção é uma boa escolha se o aplicativo autentica com uma combinação de nome de usuário e senha em vez de tokens de acesso ou cabeçalhos. Com baseado em senha de logon, os usuários precisam ter toosign de saudação do aplicativo toohello primeira vez que o acessarem. Depois disso, o Active Directory do Azure fornece Olá username e password em nome de usuário de saudação. 

Para obter informações sobre a configuração de logon baseado em senha, consulte [Compartimentação de senhas para logon único com Proxy de Aplicativo](application-proxy-sso-azure-portal.md).

## <a name="linked-sign-on"></a>Logon vinculado

Se você já tiver uma solução de logon único configurada para as identidades locais, escolha **Logon vinculado**. Essa opção permite soluções existentes de SSO do Active Directory do Azure tooleverage, mas ainda oferece aos usuários aplicativos de toohello de acesso remoto. 

Para obter informações sobre logon vinculado (antigamente conhecido como logon único existente), confira [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="integrated-windows-authentication"></a>Autenticação Integrada do Windows

Se seus aplicativos de locais usam Authentication(IWA) integrada do Windows ou se você quiser toouse a delegação restrita de Kerberos (KCD) para o logon único, escolha **autenticação integrada do Windows**. Com essa opção, os usuários precisam apenas tooauthenticate tooAzure do Active Directory e, em seguida, o conector de Proxy de aplicativo hello representa Olá usuário tooget um token Kerberos e entrar no aplicativo toohello. 

Para obter informações sobre como configurar a autenticação integrada do Windows, consulte [Delegação restrita de Kerberos para logon único com o Proxy de Aplicativo](active-directory-application-proxy-sso-using-kcd.md).

## <a name="header-based-sign-on"></a>Logon baseado em cabeçalho 

Se seus aplicativos usam cabeçalhos para autenticação, escolha **logon baseado em cabeçalho**. Com essa opção, os usuários precisam apenas tooauthentication Olá Active Directory do Azure. Parceiros da Microsoft com um serviço de autenticação de terceiros chamado PingAccess, que é convertido de token de acesso do Active Directory do Azure Olá em um formato de cabeçalho para o aplicativo hello. 

Para obter informações sobre como configurar a autenticação baseada em cabeçalho, consulte [ Autenticação baseada em cabeçalho para logon único com o Proxy de Aplicativo](application-proxy-ping-access.md).

## <a name="next-steps"></a>Próximas etapas

- [Compartimentação de senhas para logon único com o Proxy de Aplicativo](application-proxy-sso-azure-portal.md)
- [Delegação restrita de Kerberos para logon único com o Proxy de Aplicativo](active-directory-application-proxy-sso-using-kcd.md)
- [Autenticação baseada em cabeçalho para logon único com o Proxy de Aplicativo](application-proxy-ping-access.md) 
