---
title: "Azure AD Connect: Autenticação de Passagem – como ela funciona? | Microsoft Docs"
description: "Este artigo descreve como a Autenticação de Passagem do Azure Active Directory funciona."
services: active-directory
keywords: "Autenticação de Passagem do Azure AD Connect, instalar o Active Directory, componentes necessários para o Azure AD, SSO, Logon único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a>Autenticação de Passagem do Azure Active Directory: aprofundamento técnico

>[!IMPORTANT]
>A autenticação de passagem do Azure AD está atualmente na versão prévia. 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a>Como a Autenticação de Passagem do Azure Active Directory funciona?

Quando um usuário tenta toosign em um aplicativo protegido pelo Azure Active Directory (AD do Azure) e se a autenticação de passagem está habilitada no locatário hello, Olá ocorrem as seguintes etapas:

1. usuário de saudação tenta tooaccess um aplicativo (por exemplo, Olá Outlook Web App - https://outlook.office365.com/owa/).
2. Se o usuário Olá não tiver entrado, usuário Olá é redirecionado toohello AD do Azure-página de entrada.
3. usuário Olá insere seu nome de usuário e senha na página de entrada do AD do Azure de saudação e clica em botão de "Entrar" hello.
4. AD do Azure, durante o recebimento de saudação solicitação de entrada, coloca Olá nome de usuário e senha (criptografada usando uma chave pública) em uma fila.
5. Um agente de autenticação de passagem do local faz com que uma fila de toohello de chamada de saída e recupera Olá nome de usuário e a senha criptografada.
6. Agente de saudação descriptografa senha hello usando sua chave privada.
7. Agente de Hello, em seguida, valida a saudação de nome de usuário e senha no Active Directory usando APIs padrão do Windows (um toowhat mecanismo semelhante é usado pelos serviços de Federação do Active Directory). Olá nome de usuário pode ser qualquer nome de usuário Olá no local padrão (geralmente `userPrincipalName`) ou outro atributo configurado no Azure AD Connect (conhecido como `Alternate ID`).
8. Olá Active Directory Domain Controller (DC) local, em seguida, avalia Olá solicitação e retorna Olá resposta apropriada (êxito, falha, a senha expirou ou usuário bloqueado) toohello agente.
9. Agente de Hello, por sua vez, retorna esse tooAzure voltar de resposta AD.
10. AD do Azure avalia resposta hello e responde toohello usuário conforme apropriado - por exemplo, ele entra usuário Olá imediatamente ou solicitações de autenticação multifator (MFA).
11. Se Olá usuário entrar for bem-sucedida, o usuário de saudação é tooaccess capaz de aplicativo de hello.

Olá diagrama a seguir ilustra todos os componentes de saudação e etapas de saudação envolvidos.

![Autenticação de Passagem](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a>Próximas etapas
- [**Limitações atuais**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) – esse recurso está na versão prévia no momento. Saiba quais cenários têm suporte e quais não têm.
- [**Início rápido**](active-directory-aadconnect-pass-through-authentication-quick-start.md) – instale e execute a autenticação de passagem do Azure AD.
- [**Perguntas frequentes sobre** ](active-directory-aadconnect-pass-through-authentication-faq.md) -respostas toofrequently perguntas frequentes.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Saiba como tooresolve comum problemas com o recurso de saudação.
- [**SSO contínuo do Azure AD**](active-directory-aadconnect-sso.md) – Saiba mais sobre esse recurso complementar.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.
