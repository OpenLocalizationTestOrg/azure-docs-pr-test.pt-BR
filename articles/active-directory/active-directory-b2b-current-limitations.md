---
title: "aaaLimitations de colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "Limitações atuais à colaboração B2B do Azure Active Directory"
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
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a>Limitações da colaboração B2B do Azure AD
Colaboração B2B do Active Directory (AD do Azure) do Azure está atualmente limitações do assunto toohello descritas neste artigo.

## <a name="possible-double-multi-factor-authentication"></a>Possível autenticação multifator dupla
Com o Azure AD B2B, você pode impor autenticação multifator na organização do recurso hello (Olá convidar organização). motivos Olá para essa abordagem são detalhados no [acesso condicional para usuários de colaboração B2B](active-directory-b2b-mfa-instructions.md). Se um parceiro já tiver configurado e aplicadas a autenticação multifator, seus usuários podem ter autenticação de saudação tooperform uma vez em sua organização inicial e, em seguida, novamente no seu.

## <a name="instant-on"></a>Instant-on
Em fluxos de colaboração B2B do hello, vamos adicionar usuários toohello diretório e dinamicamente atualizá-los durante o resgate de convite, atribuição de aplicativo e assim por diante. Olá atualizações e gravações normalmente acontecem na instância de um diretório e devem ser replicadas em todas as instâncias. A replicação estará concluída quando todas as instâncias estiverem atualizadas. Às vezes, quando objeto Olá é gravado ou atualizado em uma instância e Olá chamar tooretrieve esse objeto é instância tooanother, latências de replicação podem ocorrer. Se isso acontecer, atualize ou tente novamente toohelp. Se você estiver escrevendo um aplicativo usando nossa API, novas tentativas com alguns retirada é uma boa prática defesa tooalleviate esse problema.

## <a name="next-steps"></a>Próximas etapas

Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:

* [O que é a colaboração B2B do AD do Azure?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Propriedades de usuário de colaboração B2B](active-directory-b2b-user-properties.md)
* [Adicionando uma função de tooa de usuário de colaboração B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegar convites de colaboração B2B](active-directory-b2b-delegate-invitations.md)
* [Grupos dinâmicos e colaboração B2B](active-directory-b2b-dynamic-groups.md)
* [Código de colaboração B2B e exemplos do PowerShell](active-directory-b2b-code-samples.md)
* [Configurar aplicativos SaaS para colaboração B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokens de usuário de colaboração B2B](active-directory-b2b-user-token.md)
* [Mapeamento de declarações de usuário de colaboração B2B](active-directory-b2b-claims-mapping.md)
* [Compartilhamento externo do Office 365](active-directory-b2b-o365-external-user.md)
