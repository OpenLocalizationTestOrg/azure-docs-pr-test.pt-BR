---
title: "Expressões condicionais do mecanismo de regras da CDN do Azure | Microsoft Docs"
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
ms.openlocfilehash: 57e56c38e003cb83dcf44f455c4451d159db8a59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="d4ec4-103">Expressões condicionais do mecanismo de regras da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="d4ec4-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="d4ec4-104">Este tópico lista descrições detalhadas das Expressões condicionais para o [Mecanismo de regras](cdn-rules-engine.md) da CDN (Rede de Distribuição de Conteúdo) do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4ec4-104">This topic lists detailed descriptions of the Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="d4ec4-105">A primeira parte de uma regra é a Expressão condicional.</span><span class="sxs-lookup"><span data-stu-id="d4ec4-105">The first part of a rule is the Conditional Expression.</span></span>

<span data-ttu-id="d4ec4-106">Expressão condicional</span><span class="sxs-lookup"><span data-stu-id="d4ec4-106">Conditional Expression</span></span> | <span data-ttu-id="d4ec4-107">Descrição</span><span class="sxs-lookup"><span data-stu-id="d4ec4-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="d4ec4-108">IF</span><span class="sxs-lookup"><span data-stu-id="d4ec4-108">IF</span></span> | <span data-ttu-id="d4ec4-109">Uma expressão IF é sempre uma parte da primeira instrução em uma regra.</span><span class="sxs-lookup"><span data-stu-id="d4ec4-109">An IF expression is always a part of the first statement in a rule.</span></span> <span data-ttu-id="d4ec4-110">Como todas as outras expressões condicionais, essa instrução IF deve ser associada a uma correspondência.</span><span class="sxs-lookup"><span data-stu-id="d4ec4-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="d4ec4-111">Se nenhuma expressão condicional adicional for definida, essa correspondência determinará o critério que deve ser atendido antes que um conjunto de recursos possa ser aplicado a uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="d4ec4-111">If no additional conditional expressions are defined, then this match determines the criterion that must be met before a set of features may be applied to a request.</span></span>
<span data-ttu-id="d4ec4-112">AND IF</span><span class="sxs-lookup"><span data-stu-id="d4ec4-112">AND IF</span></span> | <span data-ttu-id="d4ec4-113">Uma expressão AND IF só pode ser adicionada após os seguintes tipos de expressões condicionais: IF e AND IF.</span><span class="sxs-lookup"><span data-stu-id="d4ec4-113">An AND IF expression may only be added after the following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="d4ec4-114">Ela indica que há outra condição que deve ser atendida para a instrução IF inicial.</span><span class="sxs-lookup"><span data-stu-id="d4ec4-114">It indicates that there is another condition that must be met for the initial IF statement.</span></span>
<span data-ttu-id="d4ec4-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="d4ec4-115">ELSE IF</span></span>| <span data-ttu-id="d4ec4-116">Uma expressão ELSE IF especifica uma condição de alternativa que deve ser atendida antes da ocorrência de um conjunto de recursos específicos a essa instrução ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="d4ec4-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific to this ELSE IF statement takes place.</span></span> <span data-ttu-id="d4ec4-117">A presença de uma instrução ELSE IF indica o fim da instrução anterior.</span><span class="sxs-lookup"><span data-stu-id="d4ec4-117">The presence of an ELSE IF statement indicates the end of the previous statement.</span></span> <span data-ttu-id="d4ec4-118">A única expressão condicional que pode ser colocada após uma instrução ELSE IF é outra instrução ELSE IF.</span><span class="sxs-lookup"><span data-stu-id="d4ec4-118">The only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="d4ec4-119">Isso significa que uma instrução ELSE IF só pode ser usada para especificar uma única condição adicional que deve ser atendida.</span><span class="sxs-lookup"><span data-stu-id="d4ec4-119">This means that an ELSE IF statement may only be used to specify a single additional condition that has to be met.</span></span>

<span data-ttu-id="d4ec4-120">**Exemplo**: ![Condição de correspondência CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="d4ec4-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="d4ec4-121">Uma regra subsequente poderá substituir as ações especificadas por uma regra anterior.</span><span class="sxs-lookup"><span data-stu-id="d4ec4-121">A subsequent rule may override the actions specified by a previous rule.</span></span> <span data-ttu-id="d4ec4-122">Exemplo: uma regra capturar tudo protege todas as solicitações por meio da Autenticação baseada em Token.</span><span class="sxs-lookup"><span data-stu-id="d4ec4-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="d4ec4-123">Outra regra pode ser criada diretamente abaixo dessa, para criar uma exceção para determinados tipos de solicitações.</span><span class="sxs-lookup"><span data-stu-id="d4ec4-123">Another rule may be created directly below it to make an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="d4ec4-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4ec4-124">Next steps</span></span>
* [<span data-ttu-id="d4ec4-125">Visão geral da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="d4ec4-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="d4ec4-126">Referência do Mecanismo de Regras</span><span class="sxs-lookup"><span data-stu-id="d4ec4-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="d4ec4-127">Condições de correspondência do Mecanismo de regras</span><span class="sxs-lookup"><span data-stu-id="d4ec4-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="d4ec4-128">Recursos do Mecanismo de regras</span><span class="sxs-lookup"><span data-stu-id="d4ec4-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="d4ec4-129">Substituindo o comportamento HTTP padrão usando o mecanismo de regras</span><span class="sxs-lookup"><span data-stu-id="d4ec4-129">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
