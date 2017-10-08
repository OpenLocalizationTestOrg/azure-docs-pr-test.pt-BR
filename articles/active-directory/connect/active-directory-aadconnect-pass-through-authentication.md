---
title: "Azure AD Connect: autenticação de passagem | Microsoft Docs"
description: "Este artigo descreve a autenticação de passagem do Azure AD (Azure Active Directory) e como ela permite entradas do Azure AD por meio da validação de senhas de usuários no Active Directory local."
services: active-directory
keywords: "o que é a autenticação de passagem do Azure AD Connect, instalar o Active Directory, componentes necessários do Azure AD, SSO, Logon Único"
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
ms.openlocfilehash: 56cfb2c4f4afc7d46c926a392ae6ec01e96224d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="user-sign-in-with-azure-active-directory-pass-through-authentication"></a>Entrada do usuário com autenticação de passagem do Azure Active Directory

## <a name="what-is-azure-active-directory-pass-through-authentication"></a>O que é a autenticação de passagem do Azure Active Directory?

Autenticação de passagem do Azure Active Directory (AD do Azure) permite que seus usuários toosign tooboth locais e aplicativos baseados em nuvem usando Olá mesmas senhas. Esse recurso fornece aos usuários uma experiência melhor - um menos tooremember de senha e reduz os custos de suporte técnico de TI, como os usuários são menos provável tooforget como toosign no. Quando os usuários entram usando o Azure AD, esse recurso valida as senhas dos usuários diretamente no seu Active Directory local.

Esse recurso é uma alternativa muito[sincronização de Hash de senha do AD do Azure](active-directory-aadconnectsync-implement-password-synchronization.md), que fornece Olá mesmo benefício de tooorganizations de autenticação de nuvem. No entanto, as políticas de conformidade e segurança em certas organizações não permitirem essas organizações senhas de usuários toosend, mesmo em um formulário de hash, fora de seus limites internos. Autenticação de passagem é a solução certa hello para empresas desse tipo.

![O que é a Autenticação de Passagem do Azure AD](./media/active-directory-aadconnect-pass-through-authentication/pta1.png)

Você pode combinar a autenticação de passagem com hello [logon único perfeita](active-directory-aadconnect-sso.md) recurso. Dessa forma, quando os usuários acessam aplicativos em seus computadores corporativos dentro da rede corporativa, eles não precisam de tootype em toosign suas senhas no.

>[!IMPORTANT]
>A autenticação de passagem do Azure AD está atualmente na versão prévia.

## <a name="key-benefits-of-using-azure-ad-pass-through-authentication"></a>Principais benefícios de usar a Autenticação de Passagem do Azure AD

- *Ótima experiência do usuário*
  - Os usuários usam Olá mesmo toosign senhas no local e aplicativos baseados em nuvem.
  - Os usuários perdem menos tempo falando toohello assistência técnica de TI Resolvendo problemas relacionados a senha.
  - Os usuários podem concluir [gerenciamento de senha de autoatendimento](../active-directory-passwords-overview.md) tarefas na nuvem hello.
- *Fácil toodeploy & administrar*
  - Não são necessárias implantações locais ou configurações de rede complexas.
  - Precisa apenas um toobe do agente leve instalado localmente.
  - Não há sobrecarga de gerenciamento. Agente de saudação recebe automaticamente melhorias e correções de bugs.
- *Proteger*
  - Senhas locais nunca são armazenadas na nuvem de saudação de qualquer forma.
  - Agente de saudação faz apenas conexões de saída de dentro de sua rede. Portanto, não há nenhum agente de saudação do requisito tooinstall em uma rede de perímetro, também conhecida como uma rede de Perímetro.
  - Proteja suas contas de usuário trabalhando diretamente com as [Políticas de acesso condicional do Azure AD](../active-directory-conditional-access-azure-portal.md), incluindo a MFA (Autenticação Multifator), e [filtrando ataques de senha de força bruta](active-directory-aadconnect-pass-through-authentication-smart-lockout.md).
- *Altamente disponível*
  - Agentes adicionais podem ser instalados em vários locais servidores tooprovide alta disponibilidade das solicitações de entrada.

## <a name="feature-highlights"></a>Destaques do recurso

- Dá suporte à entrada do usuário em todos os aplicativos baseados em navegador da Web e em aplicativos de cliente do Microsoft Office que usam [autenticação moderna](https://aka.ms/modernauthga).
- Nomes de entrada podem ser qualquer nome de usuário Olá no local padrão (`userPrincipalName`) ou outro atributo configurado no Azure AD Connect (conhecido como `Alternate ID`).
- Olá recurso funciona perfeitamente com [acesso condicional](../active-directory-conditional-access.md) recursos como autenticação multifator (MFA) toohelp proteger seus usuários.
- Ambientes de várias florestas têm suporte se houver relações de confiança entre suas florestas do AD e se o encaminhamento de sufixo de nome estiver configurado corretamente.
- É um recurso gratuito e você não terá quaisquer edições pagas do AD do Azure toouse-lo.
- Ele pode ser habilitado por meio do [Azure AD Connect](active-directory-aadconnect.md).
- Ele usa um agente local leve que escuta e responde a solicitações de validação toopassword.
- Instalar vários agentes fornece alta disponibilidade de solicitações de entrada.
- Ele [protege](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) suas contas no local contra bruta forçar ataques de senha na nuvem hello.

## <a name="next-steps"></a>Próximas etapas

- [**Início rápido**](active-directory-aadconnect-pass-through-authentication-quick-start.md) – instale e execute a autenticação de passagem do Azure AD.
- [**Limitações atuais**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) – esse recurso está na versão prévia no momento. Saiba quais cenários têm suporte e quais não têm.
- [**Aprofundamento técnico**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) – entenda como esse recurso funciona.
- [**Perguntas frequentes sobre** ](active-directory-aadconnect-pass-through-authentication-faq.md) -respostas toofrequently perguntas frequentes.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Saiba como tooresolve comum problemas com o recurso de saudação.
- [**SSO contínuo do Azure AD**](active-directory-aadconnect-sso.md) – Saiba mais sobre esse recurso complementar.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.
