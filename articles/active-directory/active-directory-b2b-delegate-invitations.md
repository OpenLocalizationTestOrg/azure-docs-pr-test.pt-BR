---
title: "aaaDelegate convites para colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "As propriedades do usuário de colaboração B2B do Azure Active Directory podem ser configuradas"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a>Delegar convites para a colaboração do Azure Active Directory B2B

Com a colaboração de business-to-business (B2B) do Azure Active Directory (AD do Azure), você não tem toobe convites de toosend um administrador global. Em vez disso, você pode usar as políticas e delegar toousers convites cujas funções permitir que eles toosend convites. É um importante novo modo toodelegate convidado usuário convites por meio da função de emissor do convite convidado hello.

## <a name="guest-inviter-role"></a>Função Emissor do convite para convidado
Podemos atribuir Olá usuário tooGuest convites de toosend de função do emissor do convite. Você não tem membro toobe de convites de toosend de função de administrador global hello. Por padrão, usuários regulares também podem chamar a API de convite Olá a menos que um administrador global desabilitado convites para usuários regulares. Um usuário também pode chamar a API de saudação usando Olá portal do Azure ou o PowerShell.

Aqui está um exemplo que mostra como toouse PowerShell tooadd uma função do usuário toohello emissor do convite convidado:

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a>Controle quem pode convidar

![Controle como tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

Com colaboração B2B do Azure AD, um administrador de locatários pode definir Olá políticas de convite a seguir:

- Desativar convites
- Somente administradores e usuários na função de emissor do convite convidado Olá podem convidar
- Podem convidar administradores, Olá emissor do convite convidado e membros
- Todos os usuários, incluindo convidados, podem convidar

Por padrão, os locatários são definidos muito n º 4. (Todos os usuários, incluindo convidados, podem convidar usuários B2B).

## <a name="next-steps"></a>Próximas etapas

Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:

* [O que é a colaboração B2B do AD do Azure?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriedades de usuário de colaboração B2B](active-directory-b2b-user-properties.md)
* [Adicionando uma função de tooa de usuário de colaboração B2B](active-directory-b2b-add-guest-to-role.md)
* [Grupos dinâmicos e colaboração B2B](active-directory-b2b-dynamic-groups.md)
* [Código de colaboração B2B e exemplos do PowerShell](active-directory-b2b-code-samples.md)
* [Configurar aplicativos SaaS para colaboração B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokens de usuário de colaboração B2B](active-directory-b2b-user-token.md)
* [Mapeamento de declarações de usuário de colaboração B2B](active-directory-b2b-claims-mapping.md)
* [Compartilhamento externo do Office 365](active-directory-b2b-o365-external-user.md)
* [Limitações atuais da colaboração B2B](active-directory-b2b-current-limitations.md)
