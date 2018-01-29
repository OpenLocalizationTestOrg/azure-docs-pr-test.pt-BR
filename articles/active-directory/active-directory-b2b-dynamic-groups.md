---
title: "Grupos dinâmicos e Colaboração do Azure Active Directory B2B | Microsoft Docs"
description: "Mostra como usar os grupos dinâmicos do Azure AD com a colaboração B2B do Azure Active Directory"
services: active-directory
documentationcenter: 
author: sasubram
manager: mtillman
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 12/14/2017
ms.author: twooley
ms.reviewer: sasubram
ms.openlocfilehash: d60b7f70332d6183a67003c1dceb96241fc6bae4
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a>Grupos dinâmicos e Colaboração do Azure Active Directory B2B

## <a name="what-are-dynamic-groups"></a>O que são grupos dinâmicos?
A configuração dinâmica da associação de grupo de segurança para o Azure AD (Azure Active Directory) está disponível [no portal do Azure](https://portal.azure.com). Os administradores podem definir regras para preencher os grupos criados no Azure AD com base nos atributos do usuário (como userType, departamento ou país). Os membros podem ser adicionados ou removidos automaticamente de um grupo de segurança com base nas alterações de seus atributos. Esses grupos podem fornecer acesso a aplicativos ou a recursos de nuvem (como sites e documentos do SharePoint) e para atribuir licenças a membros. Leia mais sobre grupos dinâmicos em [Grupos dedicados no Azure Active Directory](active-directory-accessmanagement-dedicated-groups.md).

O [licenciamento do Azure AD Premium P1 ou P2](https://azure.microsoft.com/pricing/details/active-directory/) apropriado é necessário para criar e usar grupos dinâmicos. Saiba mais no artigo [Criar regras baseadas em atributo para associação dinâmica de grupo no Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).

## <a name="what-are-the-built-in-dynamic-groups"></a>O que são os grupos dinâmicos internos?
O grupo dinâmico **Todos os usuários**permite que administradores de locatário criem um grupo contendo todos os usuários no locatário com um único clique. Por padrão, o grupo **Todos os usuários** inclui todos os usuários no diretório, incluindo Membros e Convidados.
No novo portal de administração do Azure Active Directory, você pode optar por habilitar o grupo **Todos os usuários** na exibição Configurações de Grupo.

![Mostra habilitar o grupo Todos os Usuários definido como Sim](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

## <a name="hardening-the-all-users-dynamic-group"></a>Fortalecendo a proteção do grupo dinâmico Todos os usuários
Por padrão, o grupo **Todos os usuários** também contém os usuários de colaboração B2B (convidados). Você pode proteger ainda mais o grupo **Todos os usuários** usando uma regra para remover os usuários convidados. A ilustração a seguir mostra o grupo **Todos os usuários** modificado para excluir os convidados.

![Mostra a regra onde o tipo de usuário não é igual a convidado](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

Também pode ser útil criar um novo grupo dinâmico que contenha apenas os usuários convidados, para que você possa aplicar políticas (como as políticas de acesso condicional do Azure AD) a eles.
Como esse grupo poderia ser:

![Mostra a regra onde o tipo de usuário é igual a convidado](media/active-directory-b2b-dynamic-groups/only-guest-users.png)

## <a name="next-steps"></a>Próximas etapas

Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:

* [O que é a colaboração B2B do AD do Azure?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriedades de usuário de colaboração B2B](active-directory-b2b-user-properties.md)
* [Como adicionar um usuário de colaboração B2B a uma função](active-directory-b2b-add-guest-to-role.md)
* [Delegação de convites de colaboração B2B](active-directory-b2b-delegate-invitations.md)
* [Código de colaboração B2B e exemplos do PowerShell](active-directory-b2b-code-samples.md)
* [Configurar aplicativos SaaS para colaboração B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokens de usuário de colaboração B2B](active-directory-b2b-user-token.md)
* [Mapeamento de declarações de usuário de colaboração B2B](active-directory-b2b-claims-mapping.md)
* [Compartilhamento externo do Office 365](active-directory-b2b-o365-external-user.md)
* [Limitações atuais da colaboração B2B](active-directory-b2b-current-limitations.md)
