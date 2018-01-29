---
title: "Logon único para aplicativos com o Proxy de Aplicativo do Azure AD | Microsoft Docs"
description: "Ative o logon único para aplicativos locais publicados com o Proxy de Aplicativo do Azure AD no Portal do Azure."
services: active-directory
documentationcenter: 
author: daveba
manager: mtillman
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: daveba
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 501017ae416cc8aa473077c98ae0a213db749547
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2018
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a>Compartimentação de senhas para logon único com o Proxy de Aplicativo

O Proxy de Aplicativo do Azure Active Directory o ajuda a aprimorar a produtividade ao publicar aplicativos locais de forma que funcionários remotos também possam acessá-los com segurança. No Portal do Azure, você também pode configurar o logon único (SSO) para esses aplicativos. Os usuários só precisam autenticar com o Azure AD, assim podem acessar seu aplicativo corporativo sem precisar entrar novamente.

O Proxy de Aplicativo dá suporte a vários [modos de logon único](application-proxy-sso-overview.md). O logon único baseado em senha destina-se a aplicativos que usam uma combinação de nome de usuário e senha para autenticação. Quando você configura logon único baseado em senha para seu aplicativo, os usuários devem entrar no aplicativo local uma vez. Depois disso, o Azure Active Directory armazena as informações de entrada, fornecendo-as automaticamente ao aplicativo quando os usuários o acessarem remotamente. 

Você já deve ter publicado e testado seu aplicativo com o Proxy de Aplicativo. Caso contrário, siga as etapas em [Publicar aplicativos usando o Proxy de Aplicativo do Azure AD](application-proxy-publish-azure-portal.md) e depois volte para este artigo. 

## <a name="set-up-password-vaulting-for-your-application"></a>Definir o cofre de senha para seu aplicativo

1. Entre no [Portal do Azure](https://portal.azure.com) como administrador.
2. Selecione **Azure Active Directory** > **Aplicativos Empresariais** > **Todos os Aplicativos**.
3. Na lista, selecione o aplicativo para o qual deseja configurar o SSO.  
4. Selecione **Logon único**.

   ![Selecione Logon único](./media/application-proxy-sso-azure-portal/select-sso.png)

5. Para o modo SSO, escolha **Logon Único Baseado em Senha**.
6. Para a URL de logon, insira a URL da página em que os usuários devem inserir o nome de usuário e a senha para entrar em seu aplicativo fora da rede corporativa. Ela pode ser a URL externa criada ao publicar o aplicativo por meio do Proxy de Aplicativo. 

   ![Escolha Logon Único Baseado em Senha e digite a URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. Selecione **Salvar**.

<!-- Need to repro?
7. The page should tell you that a sign-in form was successfully detected at the provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow the instructions to point out where the sign-in credentials go. 
-->

## <a name="test-your-app"></a>Testar seu aplicativo

Vá para a URL externa que você configurou para acesso remoto ao seu aplicativo. Entre com suas credenciais do aplicativo (ou as credenciais de uma conta de teste que você configurou com acesso). Depois que você entrar com êxito, deve conseguir sair do aplicativo e voltar a ele sem ter que inserir suas credenciais novamente. 

## <a name="next-steps"></a>Próximas etapas

- Leia sobre outras maneiras de implementar o [Logon único com o Proxy de aplicativo](application-proxy-sso-overview.md)
- Saiba mais sobre [Considerações de segurança para acessar aplicativos remotamente com o Proxy de Aplicativo do Azure AD](application-proxy-security-considerations.md)