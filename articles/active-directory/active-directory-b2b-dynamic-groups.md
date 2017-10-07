---
title: "aaaDynamic grupos e colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "A colaboração B2B do Azure Active Directory pode ser usada com grupos dinâmicos do Azure AD"
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
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a>Grupos dinâmicos e Colaboração do Azure Active Directory B2B

## <a name="what-are-dynamic-groups"></a>O que são grupos dinâmicos?
Configuração dinâmica de associação de grupo de segurança do Azure Active Directory (AD do Azure) está disponível em [Olá portal do Azure](https://portal.azure.com). Os administradores podem definir regras toopopulate grupos são criados no Active Directory do Azure com base em atributos de usuário (como userType, departamento ou país). Membros podem ser adicionados automaticamente tooor removido de um grupo de segurança com base em seus atributos. Esses grupos podem fornecer acesso a recursos de nuvem ou tooapplications (sites do SharePoint, documentos) e tooassign toomembers de licenças. Leia mais sobre grupos dinâmicos em [Grupos dedicados no Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).

Olá apropriado [licenciamento do Azure AD Premium P1 ou P2](https://azure.microsoft.com/pricing/details/active-directory/) é necessário toocreate e use grupos dinâmicos. Saiba mais no artigo Olá [criar regras com base em atributo para associação de grupo dinâmico no Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).

## <a name="what-are-hello-built-in-dynamic-groups"></a>Quais são os grupos internos de dinâmico Olá?
Olá **todos os usuários** grupo dinâmico permite toocreate de administradores de inquilinos um grupo contendo todos os usuários no locatário Olá com um único clique. Por padrão, Olá **todos os usuários** grupo inclui todos os usuários no diretório hello, incluindo membros e convidados.
No portal de administração do Active Directory do Azure nova hello, você pode escolher Olá tooenable **todos os usuários** grupo Olá exibir configurações de grupo.

![grupos internos](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a>Proteção Olá grupo dinâmico de todos os usuários
Por padrão, Olá **todos os usuários** grupo contém os usuários de colaboração (convidado) B2B também. Você pode proteger ainda mais seu **todos os usuários** grupo usando usuários de convidado de tooremove uma regra. Olá, ilustração a seguir mostra Olá **todos os usuários** grupo modificado tooexclude convidados.

![habilitar o grupo todos os usuários](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

Talvez também seja útil toocreate um novo grupo dinâmico que contém apenas os usuários convidados, para que você possa aplicar políticas (como políticas de acesso condicional do Azure AD) toothem.
Como esse grupo poderia ser:

![excluir usuários convidados](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a>Próximas etapas

Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:

* [O que é a colaboração B2B do AD do Azure?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriedades de usuário de colaboração B2B](active-directory-b2b-user-properties.md)
* [Adicionando uma função de tooa de usuário de colaboração B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegação de convites de colaboração B2B](active-directory-b2b-delegate-invitations.md)
* [Código de colaboração B2B e exemplos do PowerShell](active-directory-b2b-code-samples.md)
* [Configurar aplicativos SaaS para colaboração B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokens de usuário de colaboração B2B](active-directory-b2b-user-token.md)
* [Mapeamento de declarações de usuário de colaboração B2B](active-directory-b2b-claims-mapping.md)
* [Compartilhamento externo do Office 365](active-directory-b2b-o365-external-user.md)
* [Limitações atuais da colaboração B2B](active-directory-b2b-current-limitations.md)
