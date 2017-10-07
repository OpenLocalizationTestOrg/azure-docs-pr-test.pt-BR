---
title: "aaaAdd B2B colaboração usuários tooAzure do Active Directory sem um convite | Microsoft Docs"
description: "Você pode permitir que um usuário convidado adicionar outros usuários de convidado tooyour AD do Azure sem resgatar um convite em colaboração B2B do Azure Active Directory."
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 459d99b9f856a35973d1b2cbfabdc23fe40c8f44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-b2b-collaboration-guest-users-without-an-invitation"></a>Adicionar usuários convidados da colaboração B2B sem um convite

Você pode permitir que um usuário, como um parceiro, tooadd usuários da organização do hello parceiro tooyour sem a necessidade de convites toobe resgatado. Tudo o que você deve fazer é conceder privilégios de enumeração no diretório Olá que você está usando para Olá parceiro org de usuário 

Conceda esses privilégios quando:

1. Um usuário de organização de host da saudação (por exemplo, o WoodGrove) convida um usuário da organização do parceiro de saudação (por exemplo, Sam@litware.com) como convidado.
2. Olá administrador na organização do host Olá define as políticas que permitem Sam tooidentify e adicionar outros usuários da organização do parceiro de saudação (Litware).
3. Agora o Sam pode adicionar outros usuários da Litware toohello WoodGrove diretório, grupos ou aplicativos sem a necessidade de convites toobe resgatado. Se o Sam tem privilégios de enumeração apropriado Olá no Litware, isso acontece automaticamente.

### <a name="next-steps"></a>Próximas etapas

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
* [Autenticação Multifator para usuários de colaboração B2B](active-directory-b2b-mfa-instructions.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)