---
title: "Operações do Synchronization Service Manager do Azure AD Connect | Microsoft Docs"
description: "Entenda o guia de operações Olá Olá Synchronization Service Manager para conexão do AD do Azure."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: decbc53613d456a71cd116c40c5e1fd761efd4af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-sync-service-manager-operations-tab"></a>Usando Olá guia de operações do Gerenciador de serviço de sincronização

![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

Guia de operações de saudação mostra os resultados de saudação de operações mais recentes hello. Essa guia é chave toounderstand e solucionar problemas.

## <a name="understand-hello-information-visible-in-hello-operations-tab"></a>Compreender as informações de saudação visíveis no guia de operações de saudação
metade superior Olá mostra todas as execuções em ordem cronológica. Por padrão, o log de operações Olá mantém informações sobre Olá últimos sete dias, mas essa configuração pode ser alterada com hello [Agendador](active-directory-aadconnectsync-feature-scheduler.md). Você deseja toolook para qualquer execução que não mostra um status de êxito. Você pode alterar Olá classificação clicando em cabeçalhos de saudação.

Olá **Status** coluna informações mais importantes hello e mostra Olá problema mais sério para uma execução. Aqui está um resumo de status mais comuns de saudação em ordem de prioridade tooinvestigate (onde * indicar várias cadeias de caracteres de erro possível).

| Status | Comentário |
| --- | --- |
| stopped-* |não foi possível concluir a saudação executar. Por exemplo, se hello sistema remoto está inoperante e não pode ser contatado. |
| stopped-error-limit |Há mais de 5.000 erros. Olá executar automaticamente foi interrompido devido a toohello grande número de erros. |
| completed-\*-errors |Olá execução foi concluída, mas há erros (menos de 5.000) que devem ser investigados. |
| completed-\*-warnings |Olá executar concluída, mas alguns dados não estão em estado de saudação esperado. Se houver erros, geralmente, essa mensagem indicará apenas um sintoma. Até que tenha resolvido os erros, você não deverá investigar os avisos. |
| sucesso |Nenhum problema. |

Quando você seleciona uma linha, inferior Olá atualiza tooshow detalhes de saudação do que executar. toohello à extrema esquerda da parte inferior da saudação, talvez seja necessário dizer uma lista **etapa #**. Essa lista só será exibida se você tiver vários domínios na floresta, em que cada domínio é representado por uma etapa. o nome de domínio Olá pode ser encontrado sob o título de saudação **partição**. Em **estatísticas de sincronização**, você pode encontrar mais informações sobre o número de saudação de alterações que foram processadas. Você pode clicar em Olá links tooget uma lista de objetos de saudação alterado. Se você tiver objetos com erros, eles aparecerão em **erros de sincronização**.

Para obter mais informações, consulte [Solução de problemas de um objeto que não está sincronizando](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.

Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
