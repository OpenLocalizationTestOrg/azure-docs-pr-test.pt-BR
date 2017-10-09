---
title: "aaaAzure Active Directory Identity Protection - como usuários toounblock | Microsoft Docs"
description: "Saiba como desbloquear usuários que foram bloqueados por uma política do Azure Active Directory Identity Protection."
services: active-directory
keywords: "azure active directory identity protection, desbloquear usuário"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: cdda2808822888f76aa75cf46478738c94df51a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection---how-toounblock-users"></a>Proteção do Azure Active Directory identidade - como toounblock usuários
Com o Azure Active Directory identidade Protection, você pode configurar políticas de usuários tooblock se Olá configurado condições forem atendidos. Normalmente, um usuário bloqueado contatos help desk toobecome desbloqueado. Este tópico explica as etapas de saudação você pode executar toounblock um usuário bloqueado.

## <a name="determine-hello-reason-for-blocking"></a>Determinar o motivo de saudação do bloqueio
Como uma etapa a primeira toounblock um usuário, você precisa toodetermine tipo de saudação de política que bloqueou usuário Olá porque as próximas etapas são dependem.
Com o Azure Active Directory Identity Protection, um usuário pode ser bloqueado ou por uma política de risco de entrada ou por uma política de risco de usuário.

Você pode obter o tipo de saudação de política que bloqueou a um usuário de título de saudação na caixa de diálogo Olá apresentado toohello usuário durante uma tentativa de logon:

| Política | Diálogo do usuário |
| --- | --- |
| Risco de entrada |![Entrada bloqueada](./media/active-directory-identityprotection-unblock-howto/02.png) |
| Risco do usuário |![Conta bloqueada](./media/active-directory-identityprotection-unblock-howto/104.png) |

Um usuário bloqueado por:

* Uma política de risco de entrada também é conhecida como entrada suspeita
* Uma política de risco de usuário também é conhecida como uma conta em risco

## <a name="unblocking-suspicious-sign-ins"></a>Desbloqueio de entradas suspeitas
toounblock uma entrada suspeito, você tem Olá as opções a seguir:

1. **Entrada de um local ou dispositivo familiar** - uma razão comum para entradas suspeitas bloqueadas são as tentativas de entrada de locais ou de dispositivos desconhecidos. Os usuários podem determinar rapidamente se este é o motivo de bloqueio ao tentar toosign-in de um dispositivo ou local familiar de saudação.
2. **Excluir da política** - se você achar que a configuração atual Olá de sua política de entrada está causando problemas para usuários específicos, você pode excluir usuários Olá dele. Consulte [Azure Active Directory Identity Protection](active-directory-identityprotection.md) para obter mais detalhes.
3. **Desabilitar política** - se você achar que a configuração de política está causando problemas para todos os usuários, você pode desabilitar a política de saudação. Consulte [Azure Active Directory Identity Protection](active-directory-identityprotection.md) para obter mais detalhes.

## <a name="unblocking-accounts-at-risk"></a>Desbloqueio de contas em risco
toounblock uma conta em risco, você tem Olá as opções a seguir:

1. **Redefinir senha** -você pode redefinir a senha do usuário hello. Veja [redefinição manual de senha segura](active-directory-identityprotection.md#manual-secure-password-reset) para obter mais detalhes.
2. **Ignorar todos os eventos de risco** -política de risco do usuário Olá bloqueia um usuário se o nível de risco do usuário Olá configurado para bloquear o acesso foi atingido. Você pode reduzir o nível de risco de um usuário ao fechar manualmente os eventos de risco relatados. Para obter mais detalhes, veja [fechando eventos de risco manualmente](active-directory-identityprotection.md#closing-risk-events-manually).
3. **Excluir da política** - se você achar que a configuração atual Olá de sua política de entrada está causando problemas para usuários específicos, você pode excluir usuários Olá dele. Consulte [Azure Active Directory Identity Protection](active-directory-identityprotection.md) para obter mais detalhes.
4. **Desabilitar política** - se você achar que a configuração de política está causando problemas para todos os usuários, você pode desabilitar a política de saudação. Consulte [Azure Active Directory Identity Protection](active-directory-identityprotection.md) para obter mais detalhes.

## <a name="next-steps"></a>Próximas etapas
 Você deseja tooknow mais sobre o Azure AD Identity Protection? Confira [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
