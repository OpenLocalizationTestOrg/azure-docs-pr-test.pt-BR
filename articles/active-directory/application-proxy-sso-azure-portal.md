---
title: aaaSingle logon tooapps com Proxy de aplicativo do Azure AD | Microsoft Docs
description: "Ative logon único para seus aplicativos publicados no local com o Proxy de aplicativo do Azure AD em Olá portal do Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a>Compartimentação de senhas para logon único com o Proxy de Aplicativo

O Proxy de Aplicativo do Azure Active Directory o ajuda a aprimorar a produtividade ao publicar aplicativos locais de forma que funcionários remotos também possam acessá-los com segurança. Em Olá portal do Azure, você também pode configurar único (SSO) toothese aplicativos de logon. Os usuários só precisam tooauthenticate com o Azure AD e eles podem acessar seu aplicativo empresarial sem ter toosign novamente.

O Proxy de Aplicativo dá suporte a vários [modos de logon único](application-proxy-sso-overview.md). O logon único baseado em senha destina-se a aplicativos que usam uma combinação de nome de usuário e senha para autenticação. Quando você configura com base em senha de logon para o seu aplicativo, seus usuários têm toosign no aplicativo do local toohello uma vez. Depois disso, o Active Directory do Azure armazena informações de entrada hello e automaticamente fornece toohello aplicativo quando os usuários acessam remotamente. 

Você já deve ter publicado e testado seu aplicativo com o Proxy de Aplicativo. Se não, siga as etapas de saudação em [publicar aplicativos usando o Proxy de aplicativo do Azure AD](application-proxy-publish-azure-portal.md) , em seguida, volte aqui. 

## <a name="set-up-password-vaulting-for-your-application"></a>Definir o cofre de senha para seu aplicativo

1. Entrar toohello [portal do Azure](https://portal.azure.com) como um administrador.
2. Selecione **Azure Active Directory** > **Aplicativos Empresariais** > **Todos os Aplicativos**.
3. Na lista de saudação, selecione o aplicativo hello que você deseja tooset backup com o SSO.  
4. Selecione **Logon único**.

   ![Selecione Logon único](./media/application-proxy-sso-azure-portal/select-sso.png)

5. Para o modo SSO hello, escolha **baseada em senha logon**.
6. Para Olá URL de logon, insira Olá URL para página Olá onde os usuários digitarão seu nome de usuário e senha toosign no aplicativo tooyour fora da rede corporativa hello. Isso pode ser Olá URL externa que você criou quando você publicou o aplicativo hello por meio do Proxy de aplicativo. 

   ![Escolha Logon Único Baseado em Senha e digite a URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. Selecione **Salvar**.

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a>Testar seu aplicativo

Vá tooexternal URL que você configurou para acesso remoto tooyour aplicativo. Entre com suas credenciais para esse aplicativo (ou credenciais Olá para uma conta de teste que você configurou com acesso). Depois que você entrar com êxito, você deve ser capaz de tooleave Olá aplicativo e voltar sem inserir suas credenciais novamente. 

## <a name="next-steps"></a>Próximas etapas

- Leia sobre outra maneiras tooimplement [logon único com o Proxy de aplicativo](application-proxy-sso-overview.md)
- Saiba mais sobre [Considerações de segurança para acessar aplicativos remotamente com o Proxy de Aplicativo do Azure AD](application-proxy-security-considerations.md)