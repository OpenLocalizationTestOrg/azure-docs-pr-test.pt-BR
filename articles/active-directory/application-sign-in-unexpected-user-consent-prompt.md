---
title: prompt de consentimento aaaUnexpected ao entrar no aplicativo tooan | Microsoft Docs
description: "Como tootroubleshoot quando um usuário vê um prompt de consentimento para um aplicativo que você tiver integrado ao AD do Azure que você não esperava"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a>Prompt de consentimento inesperado ao entrar no aplicativo tooan

Muitos aplicativos que se integram com o Active Directory do Azure exigem recursos toovarious permissões toorun de ordem. Quando esses recursos também são integrados com o Active Directory do Azure, permissões tooaccess-los é solicitada usando Olá AD do Azure consentimento do framework. 

Isso resulta em um prompt de consentimento sendo mostrado Olá primeira vez que um aplicativo for usado, que geralmente é uma operação única. 

## <a name="scenarios-in-which-users-see-consent-prompts"></a>Cenários nos quais os usuários visualizam solicitações de consentimento

Solicitações adicionais podem ser esperadas em vários cenários:

* Olá conjunto de permissões exigido pelo aplicativo hello foi alterado.

* usuário Olá originalmente consentimento aplicativo toohello não era um administrador, e agora um usuário diferente (não administrativa) está usando aplicativo hello para Olá primeira vez.

* usuário Olá originalmente consentimento toohello aplicativo era um administrador, mas eles não consentimento em nome de toda a organização hello.

* usando o aplicativo Hello [consentimento incremental e dinâmico](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest as permissões adicionais após a autorização inicialmente foi concedida. Isso é frequentemente usado quando recursos opcionais de um aplicativo adicional exigem permissões além das exigidas para a funcionalidade de linha de base.

* O consentimento foi revogado após ter sido inicialmente concedido.

* desenvolvedor Olá configurou Olá aplicativo toorequire uma solicitação de consentimento toda vez que ele é usado (Observação: isso não é prática recomendada).

## <a name="next-steps"></a>Próximas etapas

-   [Aplicativos, permissões e consentimento no Azure Active Directory (ponto de extremidade v1.0)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [Escopos, permissões e consentimento de saudação do Active Directory do Azure (ponto de extremidade v 2.0)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


