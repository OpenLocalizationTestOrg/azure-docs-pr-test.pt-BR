---
title: "aaaFind-out quando um usuário específico será capaz de tooaccess um aplicativo | Microsoft Docs"
description: "Como toofind-out quando um usuário criticamente importante ser capaz de tooaccess um aplicativo que você tiver configurado para provisionamento do usuário com o Azure AD"
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
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a>Descobrir quando um usuário específico será capaz de tooaccess um aplicativo
Ao usar o provisionamento automático de usuário com um aplicativo, o Azure AD automaticamente provisionar e atualizar contas de usuário em um aplicativo com base em coisas como [atribuição de usuário e grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) em um intervalo de tempo agendado regularmente, normalmente a cada 10 minutos.

## <a name="how-long-does-it-take"></a>Quanto tempo demora?

tempo de saudação que leva para um toobe de determinado usuário provisionado depende principalmente se já tiver ocorrido uma sincronização inicial de "full".

Olá primeira sincronização entre o AD do Azure e um aplicativo pode demorar horas tooseveral de 20 minutos, dependendo do tamanho de saudação do diretório de saudação do AD do Azure e número de saudação de usuários em escopo para provisionamento. 

As sincronizações subsequentes após a sincronização inicial de saudação ser mais rápido (por exemplo, em 10 minutos), como Olá provisionamento serviço armazena as marcas d'água que representam o estado de saudação de ambos os sistemas após a sincronização inicial hello, melhorando o desempenho de sincronizações subsequentes.

## <a name="how-toocheck-hello-status-of-a-user"></a>Como toocheck Olá status de um usuário

status de provisionamento toosee Olá para um usuário selecionado, consulte Olá os logs de auditoria no AD do Azure.

Olá provisionamento logs de auditoria pode ser acessada no hello portal do Azure, na Olá **Active Directory do Azure &gt; aplicativos corporativos &gt; \[nome do aplicativo\] &gt; Logs de auditoria**guia. Saudação de filtro logon Olá **provisionamento de conta** tooonly categoria consulte Olá provisionamento eventos para esse aplicativo. Você pode procurar usuários com base em hello "correspondência ID" que foi configurado para eles nos mapeamentos de atributo hello. 

Por exemplo, se você configurou hello "user principal name" ou "endereço de email" como Olá correspondência de atributo no lado de saudação do AD do Azure e não sendo provisionamento de usuário de saudação tem um valor de "audrey@contoso.com", em seguida, os logs de auditoria de saudação de pesquisa para"audrey@contoso.com" e, em seguida, examine as entradas são retornadas.

Olá provisionamento auditoria registra registro todas Olá operações executadas pelo Olá provisionamento de serviço, incluindo:

* Consultando o Azure AD para usuários atribuídos que estão no escopo de provisionamento
* Consultando o aplicativo de destino Olá existência Olá desses usuários
* Comparando objetos de usuário Olá entre sistema Olá
* Adicionar, atualizar ou desabilitar a conta de usuário de saudação no sistema de destino de saudação com base em comparação de saudação

## <a name="next-steps"></a>Próximas etapas
[Automatizar o provisionamento de usuário e desprovisionamento tooSaaS aplicativos com o Active Directory do Azure](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)'
