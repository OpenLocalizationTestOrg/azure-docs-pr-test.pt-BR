---
title: "Azure AD Connect: Logon Único Contínuo | Microsoft Docs"
description: "Este tópico descreve o Azure Active Directory (AD do Azure) perfeita Single Sign-On e como isso permite que você tooprovide true logon único para usuários corporativos de área de trabalho dentro da rede corporativa."
services: active-directory
keywords: "o que é o Azure AD Connect, instalar o Active Directory, componentes necessários do Azure AD, SSO, Logon Único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 11c778c37ee39866dcc3a14ab648cfcd8e322e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on"></a>Logon Único Contínuo do Azure Active Directory

## <a name="what-is-azure-active-directory-seamless-single-sign-on"></a>O que é o Logon Único Contínuo do Azure Active Directory?

Azure Active Directory perfeita SSO (Azure AD perfeita SSO) assina automaticamente os usuários quando eles estão na rede corporativa dispositivos corporativos tooyour conectado. Quando habilitada, os usuários não precisa tootype em toosign suas senhas no tooAzure AD e digite normalmente, mesmo em seus nomes de usuário. Este recurso fornece o acesso fácil aos usuários tooyour baseado em nuvem aplicativos sem a necessidade de todos os componentes locais adicionais.

SSO contínuo pode ser combinado com qualquer Olá [sincronização de Hash de senha](active-directory-aadconnectsync-implement-password-synchronization.md) ou [autenticação de passagem](active-directory-aadconnect-pass-through-authentication.md) métodos de entrada.

![Logon Único Contínuo](./media/active-directory-aadconnect-sso/sso1.png)

>[!IMPORTANT]
>O SSO Contínuo do Azure AD está atualmente em versão de visualização. Esse recurso é _não_ aplicável tooActive Directory Federation Services (ADFS).

## <a name="key-benefits"></a>Principais benefícios

- *Ótima experiência do usuário*
  - Os usuários são conectados automaticamente aos aplicativos baseados em nuvem e locais.
  - Os usuários não tenham tooenter suas senhas repetidamente.
- *Fácil toodeploy & administrar*
  - Nenhum componente adicional necessário local toomake esse trabalho.
  - Funciona com qualquer método de autenticação de nuvem – [Sincronização de hash de senha](active-directory-aadconnectsync-implement-password-synchronization.md) ou [Autenticação de passagem](active-directory-aadconnect-pass-through-authentication.md).
  - Pode ser implantado toosome ou todos os seus usuários usando a diretiva de grupo.
  - Registre dispositivos sem Windows 10 com o Azure AD, sem necessidade de saudação de qualquer infraestrutura do AD FS. Essa funcionalidade precisa toouse versão 2.1 ou posterior do hello [cliente de ingresso](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="feature-highlights"></a>Destaques do recurso

- Nome de logon pode ser qualquer nome de usuário Olá no local padrão (`userPrincipalName`) ou outro atributo configurado no Azure AD Connect (`Alternate ID`). Ambos usam trabalho de casos como SSO contínua usa Olá `securityIdentifier` declaração no toolook de tíquete Kerberos Olá o objeto de usuário correspondente Olá no AD do Azure.
- O SSO Contínuo é um recurso oportunista. Se ele falhar por algum motivo, experiência de entrada do usuário de saudação vai voltar comportamento normal tooits - ou seja, Olá usuário precisa tooenter sua senha na página de entrada hello.
- Se um aplicativo encaminha uma `domain_hint` (OpenID Connect) ou `whr` parâmetro (SAML) - identificar seu locatário, ou `login_hint` parâmetro - identificação de usuário hello, no seu AD do Azure solicitação de entrada, os usuários são automaticamente conectados sem eles Inserir nomes de usuário ou senhas.
- Isso pode ser habilitado por meio do Azure AD Connect.
- É um recurso gratuito e você não terá quaisquer edições pagas do AD do Azure toouse-lo.
- Há suporte para ele em clientes baseados em navegador da Web e clientes do Office que dão suporte à [autenticação moderna](https://aka.ms/modernauthga) em plataformas e navegadores que sejam compatíveis com a autenticação Kerberos:

| Sistema operacional\Navegador |Internet Explorer|Edge|Google Chrome|Mozilla Firefox|Safari|
| --- | --- |--- | --- | --- | -- 
|Windows 10|Sim|Não|Sim|Sim\*|N/D
|Windows 8.1|Sim|N/D|Sim|Sim\*|N/D
|Windows 8|Sim|N/D|Sim|Sim\*|N/D
|Windows 7|Sim|N/D|Sim|Sim\*|N/D
|Mac OS X|N/D|N/D|Sim\*|Sim\*|Sim\*

\*Exige [configuração adicional](active-directory-aadconnect-sso-quick-start.md#browser-considerations)

>[!IMPORTANT]
>Podemos recentemente revertida suporte para a borda tooinvestigate problemas reportados por clientes.

>[!NOTE]
>Para Windows 10, a recomendação de saudação é toouse [junção do Azure AD](../active-directory-azureadjoin-overview.md) para Olá ideal única experiência de logon com o Azure AD.

## <a name="next-steps"></a>Próximas etapas

- [**Início Rápido** ](active-directory-aadconnect-sso-quick-start.md) – colocar o SSO Contínuo do Azure AD em funcionamento.
- [**Aprofundamento técnico**](active-directory-aadconnect-sso-how-it-works.md) – entenda como esse recurso funciona.
- [**Perguntas frequentes sobre** ](active-directory-aadconnect-sso-faq.md) -respostas toofrequently perguntas frequentes.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-sso.md) -Saiba como tooresolve comum problemas com o recurso de saudação.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.
