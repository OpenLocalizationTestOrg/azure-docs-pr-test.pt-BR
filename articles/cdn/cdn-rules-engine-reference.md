---
title: "referência do mecanismo de regras de aaaAzure CDN | Microsoft Docs"
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
ms.openlocfilehash: 4159715d15fc792afb49dcd2a30752fabcd94a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine"></a>Mecanismo de regras da CDN do Azure
Este tópico lista as descrições detalhadas das condições de correspondência disponíveis hello e recursos para o Azure Content Delivery Network (CDN) [mecanismo de regras](cdn-rules-engine.md).

Olá mecanismo de regras de HTTP é projetado toobe Olá final autoridade em tipos específicos de solicitações processadas pelo Olá CDN.

**Usos comuns**:

- Substituir ou definir uma política de cache personalizada.
- Proteger ou negar solicitações de conteúdo confidencial.
- Solicitações de redirecionamento.
- Armazenar dados de log personalizados.

## <a name="terminology"></a>Terminologia
Uma regra é definida por meio do uso de saudação do [ **expressões condicionais**](cdn-rules-engine-reference-conditional-expressions.md), [ **corresponde**](cdn-rules-engine-reference-match-conditions.md), e [  **recursos**](cdn-rules-engine-reference-features.md). Esses elementos são realçados em Olá ilustração a seguir.

 ![Condição de correspondência CDN](./media/cdn-rules-engine-reference/cdn-rules-engine-terminology.png)

## <a name="syntax"></a>Sintaxe

no qual os caracteres especiais serão tratados de maneira de Hello varia acordo toohow um critério de correspondência ou valores de texto de identificadores de recurso. Uma condição de correspondência ou um recurso pode interpretar o texto em uma saudação maneiras a seguir:

1. [**Valores literais**](#literal-values) 
2. [**Valores de caractere curinga**](#wildcard-values)
3. [**Expressões regulares**](#regular-expressions)

### <a name="literal-values"></a>Valores literais
Texto que é interpretado como um valor literal tratará todos os caracteres especiais, com exceção de saudação do símbolo de % hello, como parte do valor de saudação que deve ser correspondentes. Em outras palavras, um literal coincidir com a condição definida muito`\'*'\` somente será satisfeita quando o valor que exato (ou seja, `\'*'\`) foi encontrado.
 
Um símbolo de porcentagem é a URL usada tooindicate codificação (por exemplo, `%20`).

### <a name="wildcard-values"></a>Valores de caractere curinga
Texto que é interpretado como um valor curinga atribuirá caracteres de toospecial significado adicional. Olá, a tabela a seguir descreve como Olá após o conjunto de caracteres será interpretada.

Character | Descrição
----------|------------
\ | Uma barra invertida é usada tooescape caracteres hello especificadas nesta tabela. Uma barra invertida deve ser especificada antes de caractere especial de saudação que deve ser substituído.<br/>Por exemplo, Olá sintaxe a seguir ignora um asterisco:`\*`
% | Um símbolo de porcentagem é a URL usada tooindicate codificação (por exemplo, `%20`).
* | Um asterisco é um caractere curinga que representa um ou mais caracteres.
Espaço | Um caractere de espaço indica que uma condição de correspondência pode ser satisfeita uma saudação especificada valores ou padrões.
'valor' | As aspas simples não têm significado especial. No entanto, um conjunto de aspas simples é usado tooindicate um valor deve ser tratado como um valor literal. Ele pode ser usado em Olá maneiras a seguir:<br><br/>-Permite que um toobe de condição de correspondência atendidas sempre que Olá qualquer parte do valor de comparação de saudação de correspondências de valor especificado.  Por exemplo, `'ma'` seria corresponde a nenhum dos Olá cadeias de caracteres a seguir: <br/><br/>/business/**ma**rathon/asset.htm<br/>**ma**p.gif<br/>/business/template.**ma**p<br /><br />-Permite que um toobe caractere especial especificado como um caractere literal. Por exemplo, você pode especificar um caractere de espaço literal colocando um caractere de espaço dentro de um conjunto de aspas simples (ou seja, `' '` ou `'sample value'`).<br/>-Permite que um toobe de valor em branco especificado. Especifique um valor em branco especificando um conjunto de aspas simples (ou seja, '').<br /><br/>**Importante:**<br/>-Se Olá especificado valor não contém um caractere curinga, em seguida, será automaticamente considerado um valor literal. Isso significa que não é necessário toospecify um conjunto de aspas simples.<br/>- Se uma barra invertida não funcionar como escape para outro caractere nesta tabela, ele será ignorado quando especificado dentro de um conjunto de aspas simples.<br/>-Outra maneira toospecify um caractere especial como um caractere literal é tooescape-lo usando uma barra invertida (ou seja, `\`).

### <a name="regular-expressions"></a>Expressões regulares

As expressões regulares definem um padrão que será pesquisado em um valor de texto. Notação de expressão regular define vários significados específicos tooa símbolos. Olá, tabela a seguir indica os caracteres especiais como são tratados por condições de correspondência e recursos que oferecem suporte a expressões regulares.

Caractere especial | Descrição
------------------|------------
\ | Uma barra invertida escapes Olá caractere Olá segue. Isso faz com que essa toobe de caractere tratado como um valor literal em vez de usar em seu significado de expressão regular. Por exemplo, Olá sintaxe a seguir ignora um asterisco:`\*`
% | significado Olá um símbolo de porcentagem depende de seu uso.<br/><br/> `%{HTTPVariable}`: essa sintaxe identifica uma variável HTTP.<br/>`%{HTTPVariable%Pattern}`: Esta sintaxe usa um símbolo de porcentagem tooidentify um HTTP, variável e como um delimitador.<br />`\%`: Ignorando um símbolo de porcentagem permite toobe usado como um valor literal ou uma codificação de URL tooindicate (por exemplo, `\%20`).
* | Um asterisco permite Olá anterior toobe de caractere que corresponde a zero ou mais vezes. 
Espaço | Normalmente, um caractere de espaço é tratado como um caractere literal. 
'valor' | Aspas simples são tratadas como caracteres literais. Um conjunto de aspas simples não tem significado especial.


## <a name="next-steps"></a>Próximas etapas
* [Condições de correspondência do Mecanismo de regras](cdn-rules-engine-reference-match-conditions.md)
* [Expressões condicionais do Mecanismo de regras](cdn-rules-engine-reference-conditional-expressions.md)
* [Recursos do Mecanismo de regras](cdn-rules-engine-reference-features.md)
* [Substituindo o comportamento HTTP padrão usando o mecanismo de regras de saudação](cdn-rules-engine.md)
* [Visão geral da CDN do Azure](cdn-overview.md)
