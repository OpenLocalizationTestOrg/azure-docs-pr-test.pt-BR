---
title: "aaaConditional acesso para usuários de colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "Colaboração B2B do Active Directory do Azure oferece suporte a autenticação multifator (MFA) para aplicativos corporativos do acesso seletivo tooyour"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a>Acesso condicional para usuários de colaboração B2B

## <a name="multi-factor-authentication-for-b2b-users"></a>Autenticação multifator para usuários B2B
Com a colaboração B2B do Azure AD, as organizações podem aplicar políticas de MFA (autenticação multifator) para usuários B2B. Essas políticas podem ser aplicadas no locatário hello, aplicativo ou nível de usuário individual, hello mesma forma que são habilitadas para funcionários em tempo integral e os membros da organização hello. MFA políticas são aplicadas na organização do recurso de saudação.

Exemplo:
1. Trabalho de administração ou informações na empresa A convida usuário do aplicativo de tooan empresa B *Foo* na empresa A.
2. Aplicativo *Foo* na empresa A é configurado toorequire MFA acesso.
3. Quando o usuário de saudação da empresa B tenta aplicativo tooaccess *Foo* na empresa Olá um locatário, eles são frequentes toocomplete um desafio MFA.
4. Olá usuário pode configurar o MFA com a empresa e escolhe a opção de MFA.
5. Esse cenário funciona para qualquer identidade (Azure AD ou MSA, por exemplo, se os usuários na Empresa B autenticarem usando a ID social)
6. A empresa A deve ter licenças suficientes do Azure AD Premium que oferecem suporte a MFA. usuário de saudação da empresa B consome esta licença da empresa A.

Aluguel convidar Olá sempre é responsável por MFA para usuários da organização do parceiro hello, mesmo se a organização do parceiro de saudação tem recursos MFA.

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a>Definindo a MFA para usuários de colaboração B2B
toodiscover como tooset a MFA para usuários de colaboração B2B, é fácil ver como em Olá vídeo a seguir:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a>Experiência de MFA de usuários B2B para resgate de oferta
Check-out Olá experiência de resgate animação toosee Olá a seguir:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a>Redefinição de MFA para usuários de colaboração B2B
Atualmente, Olá administrador pode exigir tooproof de usuários de colaboração B2B backup novamente usando Olá cmdlets do PowerShell a seguir:

1. Conecte-se tooAzure AD

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. Obter todos os usuários com métodos de verificação

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  Aqui está um exemplo:

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. Redefina o método MFA hello para métodos um usuário específico toorequire Olá B2B colaboração usuário tooset prova-up novamente. Exemplo:

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a>Por que realizamos MFA no aluguel de recurso Olá?

Na versão atual do hello, MFA é sempre de aluguel de recurso hello, por motivos de previsibilidade. Por exemplo, digamos que um usuário Contoso (Sally) é tooFabrikam convidado e Fabrikam habilitou MFA para usuários de B2B.

Se Contoso política da MFA habilitada para o App1, mas não App2, em seguida, se observarmos Olá declaração Contoso MFA no token de saudação pode vemos Olá problema a seguir:

* Dia 1: um usuário tem MFA na Contoso e está acessando o App1, então nenhuma solicitação de MFA adicional é mostrada na Fabrikam.

* Dia 2: Olá usuário acessou 2 de aplicativo na Contoso, agora ao acessar a Fabrikam, eles devem se registrar para MFA existe.

Esse processo pode ser confuso e causar toodrop na entrada conclusões.

Além disso, mesmo que a Contoso tem a capacidade MFA, nem sempre é Olá Olá caso Fabrikam deve confiar Olá política da MFA da Contoso.

Finalmente, a MFA de locatários de recursos também funciona para IDs sociais e MSAs e para organizações parceiras que não tenham a MFA configurada.

Portanto, a recomendação Olá para MFA para usuários de B2B é tooalways exigir a MFA no hello convidar locatário. Esse requisito pode causar toodouble MFA em alguns casos, mas sempre que acessar o locatário convidar Olá, experiência de usuários finais Olá é previsível: Sally deve registrar para MFA com locatário convidar hello.

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a>Acesso condicional com base em risco, no local e no dispositivo para usuários B2B

Quando Contoso permite que as políticas de acesso condicional com base no dispositivo para seus dados corporativos, acesso será impedido de dispositivos que não são gerenciados pela Contoso e não compatíveis com políticas de dispositivo Olá Contoso.

Se o dispositivo do usuário Olá B2B não é gerenciado pela Contoso, acesso de usuários de B2B de organizações de parceiros de saudação é bloqueado em qualquer contexto essas políticas são aplicadas. No entanto, a Contoso pode criar exclusão listas contendo tooexclude de usuários do parceiro específico de Olá política de acesso condicional com base no dispositivo.

#### <a name="location-based-conditional-access-for-b2b"></a>Acesso condicional com base em local para B2B

Políticas de acesso condicional com base no local podem ser impostas para usuários de B2B se a organização convidar Olá é capaz de toocreate um intervalo de endereços IP confiável que define suas organizações de parceiro.

#### <a name="risk-based-conditional-access-for-b2b"></a>Acesso condicional com base em risco para B2B

No momento, políticas com base em risco de entrada não podem ser aplicado tooB2B usuários porque avaliação de risco hello está sendo executada na organização inicial do usuário Olá B2B.

## <a name="next-steps"></a>Próximas etapas

Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:

* [O que é a colaboração B2B do AD do Azure?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?](active-directory-b2b-admin-add-users.md)
* [Como os operadores de informação adicionam usuários de colaboração B2B?](active-directory-b2b-iw-add-users.md)
* [elementos de saudação do hello email de convite de colaboração B2B](active-directory-b2b-invitation-email.md)
* [Resgate de convite de colaboração B2B](active-directory-b2b-redemption-experience.md)
* [Licenciamento da colaboração B2B do Azure AD](active-directory-b2b-licensing.md)
* [Solução de problemas de colaboração B2B do Azure Active Directory](active-directory-b2b-troubleshooting.md)
* [Perguntas frequentes sobre a colaboração B2B do Azure Active Directory](active-directory-b2b-faq.md)
* [API e personalização da colaboração B2B do Azure Active Directory](active-directory-b2b-api.md)
* [Adicionar usuários de colaboração B2B sem um convite](active-directory-b2b-add-user-without-invite.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
