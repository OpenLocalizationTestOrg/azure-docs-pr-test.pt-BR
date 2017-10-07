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
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="c0c82-103">Expressões condicionais do mecanismo de regras da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="c0c82-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="c0c82-104">Este tópico lista as descrições detalhadas dos Olá expressões condicionais para o Azure Content Delivery Network (CDN) [mecanismo de regras](cdn-rules-engine.md).</span><span class="sxs-lookup"><span data-stu-id="c0c82-104">This topic lists detailed descriptions of hello Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="c0c82-105">Olá primeira parte de uma regra é Olá expressão condicional.</span><span class="sxs-lookup"><span data-stu-id="c0c82-105">hello first part of a rule is hello Conditional Expression.</span></span>

<span data-ttu-id="c0c82-106">Expressão condicional</span><span class="sxs-lookup"><span data-stu-id="c0c82-106">Conditional Expression</span></span> | <span data-ttu-id="c0c82-107">Descrição</span><span class="sxs-lookup"><span data-stu-id="c0c82-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="c0c82-108">IF</span><span class="sxs-lookup"><span data-stu-id="c0c82-108">IF</span></span> | <span data-ttu-id="c0c82-109">Uma expressão IF sempre é uma parte da primeira instrução Olá em uma regra.</span><span class="sxs-lookup"><span data-stu-id="c0c82-109">An IF expression is always a part of hello first statement in a rule.</span></span> <span data-ttu-id="c0c82-110">Como todas as outras expressões condicionais, essa instrução IF deve ser associada a uma correspondência.</span><span class="sxs-lookup"><span data-stu-id="c0c82-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="c0c82-111">Se nenhuma expressão condicional adicional forem definida, essa correspondência determina o critério de saudação que deve ser atendido antes de um conjunto de recursos pode ser aplicada tooa solicitação.</span><span class="sxs-lookup"><span data-stu-id="c0c82-111">If no additional conditional expressions are defined, then this match determines hello criterion that must be met before a set of features may be applied tooa request.</span></span>
<span data-ttu-id="c0c82-112">AND IF</span><span class="sxs-lookup"><span data-stu-id="c0c82-112">AND IF</span></span> | <span data-ttu-id="c0c82-113">Uma expressão e se pode ser adicionada somente após Olá tipos de expressões condicional: IF, e se a seguir.</span><span class="sxs-lookup"><span data-stu-id="c0c82-113">An AND IF expression may only be added after hello following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="c0c82-114">Ele indica que há outra condição que deve ser atendida para a instrução IF inicial de saudação.</span><span class="sxs-lookup"><span data-stu-id="c0c82-114">It indicates that there is another condition that must be met for hello initial IF statement.</span></span>
<span data-ttu-id="c0c82-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="c0c82-115">ELSE IF</span></span>| <span data-ttu-id="c0c82-116">Uma expressão ELSE IF Especifica uma condição alternativa que deve ser atendida antes de um conjunto de recursos específico toothis instrução ELSE IF ocorre.</span><span class="sxs-lookup"><span data-stu-id="c0c82-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific toothis ELSE IF statement takes place.</span></span> <span data-ttu-id="c0c82-117">presença de saudação de uma instrução ELSE IF indica o final de saudação da instrução anterior hello.</span><span class="sxs-lookup"><span data-stu-id="c0c82-117">hello presence of an ELSE IF statement indicates hello end of hello previous statement.</span></span> <span data-ttu-id="c0c82-118">Olá expressão condicional só pode ser colocada após uma instrução ELSE IF é outra instrução ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="c0c82-118">hello only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="c0c82-119">Isso significa que uma instrução ELSE IF só pode ser usado toospecify uma única condição adicional que tenha toobe atendido.</span><span class="sxs-lookup"><span data-stu-id="c0c82-119">This means that an ELSE IF statement may only be used toospecify a single additional condition that has toobe met.</span></span>

<span data-ttu-id="c0c82-120">**Exemplo**: ![Condição de correspondência CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="c0c82-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="c0c82-121">Uma regra subsequente pode substituir ações Olá especificadas por uma regra anterior.</span><span class="sxs-lookup"><span data-stu-id="c0c82-121">A subsequent rule may override hello actions specified by a previous rule.</span></span> <span data-ttu-id="c0c82-122">Exemplo: uma regra capturar tudo protege todas as solicitações por meio da Autenticação baseada em Token.</span><span class="sxs-lookup"><span data-stu-id="c0c82-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="c0c82-123">Outra regra pode ser criada diretamente abaixo dela toomake uma exceção de certos tipos de solicitações.</span><span class="sxs-lookup"><span data-stu-id="c0c82-123">Another rule may be created directly below it toomake an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="c0c82-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c0c82-124">Next steps</span></span>
* [<span data-ttu-id="c0c82-125">Visão geral da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="c0c82-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="c0c82-126">Referência do Mecanismo de Regras</span><span class="sxs-lookup"><span data-stu-id="c0c82-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="c0c82-127">Condições de correspondência do Mecanismo de regras</span><span class="sxs-lookup"><span data-stu-id="c0c82-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="c0c82-128">Recursos do Mecanismo de regras</span><span class="sxs-lookup"><span data-stu-id="c0c82-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="c0c82-129">Substituindo o comportamento HTTP padrão usando o mecanismo de regras de saudação</span><span class="sxs-lookup"><span data-stu-id="c0c82-129">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
