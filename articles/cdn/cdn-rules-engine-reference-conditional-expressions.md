---
title: "expressões condicionais do mecanismo de regras de aaaAzure CDN | Microsoft Docs"
description: "Documentação de referência para recursos e condições de correspondência do mecanismo de regras da CDN do Azure."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 39d0754c34a577f77ca87b6fd92e2b6a9e4ff8fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a>Expressões condicionais do mecanismo de regras da CDN do Azure
Este tópico lista as descrições detalhadas dos Olá expressões condicionais para o Azure Content Delivery Network (CDN) [mecanismo de regras](cdn-rules-engine.md).

Olá primeira parte de uma regra é Olá expressão condicional.

Expressão condicional | Descrição
-----------------------|-------------
IF | Uma expressão IF sempre é uma parte da primeira instrução Olá em uma regra. Como todas as outras expressões condicionais, essa instrução IF deve ser associada a uma correspondência. Se nenhuma expressão condicional adicional forem definida, essa correspondência determina o critério de saudação que deve ser atendido antes de um conjunto de recursos pode ser aplicada tooa solicitação.
AND IF | Uma expressão e se pode ser adicionada somente após Olá tipos de expressões condicional: IF, e se a seguir. Ele indica que há outra condição que deve ser atendida para a instrução IF inicial de saudação.
ELSE IF| Uma expressão ELSE IF Especifica uma condição alternativa que deve ser atendida antes de um conjunto de recursos específico toothis instrução ELSE IF ocorre. presença de saudação de uma instrução ELSE IF indica o final de saudação da instrução anterior hello. Olá expressão condicional só pode ser colocada após uma instrução ELSE IF é outra instrução ELSE IF. Isso significa que uma instrução ELSE IF só pode ser usado toospecify uma única condição adicional que tenha toobe atendido.

**Exemplo**: ![Condição de correspondência CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)

 > [!TIP]
   > Uma regra subsequente pode substituir ações Olá especificadas por uma regra anterior. Exemplo: uma regra capturar tudo protege todas as solicitações por meio da Autenticação baseada em Token. Outra regra pode ser criada diretamente abaixo dela toomake uma exceção de certos tipos de solicitações.

### <a name="next-steps"></a>Próximas etapas
* [Visão geral da CDN do Azure](cdn-overview.md)
* [Referência do Mecanismo de Regras](cdn-rules-engine-reference.md)
* [Condições de correspondência do Mecanismo de regras](cdn-rules-engine-reference-match-conditions.md)
* [Recursos do Mecanismo de regras](cdn-rules-engine-reference-features.md)
* [Substituindo o comportamento HTTP padrão usando o mecanismo de regras de saudação](cdn-rules-engine.md)
