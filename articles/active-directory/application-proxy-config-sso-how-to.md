---
title: "aaaHow tooconfigure único logon tooan aplicativo Proxy de aplicativo | Microsoft Docs"
description: "Como você pode configurar rapidamente aplicativos de proxy de aplicativo tooyour de logon único"
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
ms.openlocfilehash: e1289203177c77b3a8bcc9058c5c0b8ae50f243e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-single-sign-on-tooan-application-proxy-application"></a>Como tooconfigure único tooan logon no aplicativo de Proxy de aplicativo

Logon único (SSO) permite que seus usuários tooaccess um aplicativo sem autenticação várias vezes. Ele permite toooccur de autenticação único Olá na nuvem hello, no Azure Active Directory e permite serviço hello ou toocomplete de usuário do conector tooimpersonate Olá os desafios de autenticação adicional do aplicativo hello.

## <a name="how-tooconfigure-single-sign-on"></a>Como tooconfigure de logon único
tooconfigure SSO, primeiro certifique-se de que seu aplicativo está configurado para pré-autenticação por meio do Active Directory do Azure. toodo, ir muito**Active Directory do Azure**  - &gt; **aplicativos empresariais**  - &gt; **todos os aplicativos**  - &gt; Seu aplicativo  **- &gt; Proxy de aplicativo**. Nessa página, você vê hello "Pré-autenticação" campo e certifique-se de que está definido muito "Active Directory do Azure. 

Para obter mais informações sobre métodos de pré-autenticação Olá, consulte a etapa quatro Olá [documento de publicação do aplicativo](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

   ![O método de pré-autenticação no Portal do Azure](./media/application-proxy-config-sso-how-to/app-proxy.png)

## <a name="configuring-single-sign-on-modes-for-application-proxy-applications"></a>Configurando modos de logon único para aplicativos do Application Proxy
Em seguida, configure tipo específico de saudação do logon único. métodos de logon da saudação são classificados com base em como o tipo de aplicativo de back-end de saudação de autenticação usado. Aplicativos de Application Proxy oferecem suporte a três tipos de logon:

-   **Com base em senha de logon**: com base em senha de logon pode ser usado para qualquer aplicativo que usa campos de nome de usuário e senha em toosign. Etapas de configuração podem ser encontradas no nosso [documentação de configuração de SSO com senha](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#bring-your-own-password-sso-applications).

-   **Autenticação integrada do Windows**: para aplicativos que usam autenticação integrada do Windows (IWA), o logon único está habilitado por meio de delegação de restrita de Kerberos (KCD). Isso permitirá que os conectores de Proxy de aplicativo no Active Directory tooimpersonate usuários e toosend e receber tokens em seu nome. Detalhes sobre como configurar o KCD podem ser encontrados no hello [logon único com documentação KCD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd).

-   **Logon com base no cabeçalho**: logon com base no cabeçalho é habilitado por meio de uma parceria e exige alguma configuração adicional. Para obter detalhes sobre a parceria de saudação e instruções passo a passo para configurar o aplicativo tooan de logon único que usa cabeçalhos de autenticação, consulte Olá [PingAccess para a documentação do AD do Azure](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).

Cada uma dessas opções pode ser encontrada, acessando o aplicativo tooyour em "Aplicativos corporativos" e saudação de abertura **Single Sign-On** página no menu esquerdo hello. Observe que, se seu aplicativo foi criado no portal antigo hello, você talvez não veja todas essas opções.

Nessa página, você também visualiza uma opção de logon adicional: logon vinculado. Isso também tem suporte pelo Application Proxy. No entanto, observe que essa opção não adiciona aplicativos toohello de logon único. Dito isso aplicativo hello pode já ter SSO implementado usando outro serviço, como os serviços de Federação do Active Directory. 

Esta opção permite a um administrador toocreate um aplicativo de tooan de link que os usuários parar em ao acessar o aplicativo hello. Por exemplo, se houver um aplicativo que é configurado tooauthenticate usuários usando o Active Directory Federation Services 2.0, um administrador pode usar o hello "vinculado logon" opção toocreate tooit um link no painel de acesso de saudação.

## <a name="next-steps"></a>Próximas etapas
[Fornecer aplicativos de tooyour de logon único com o Proxy de aplicativo](active-directory-application-proxy-sso-using-kcd.md)
