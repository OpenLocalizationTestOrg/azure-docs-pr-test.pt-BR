---
title: "aaaSet o Glossário de negócios Olá para marcação controlada no catálogo de dados do Azure | Microsoft Docs"
description: "Como tooarticle realce Glossário de saudação negócios no catálogo de dados do Azure para definir e usar um tootag de vocabulário de negócios comuns ativos de dados registrados."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: b3d63dbe-1ae7-499f-bc46-42124e950cd6
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: c9adf663bd08ac3c0c7b5d3551e6af409fe69ebc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-business-glossary-for-governed-tagging"></a>Configurar Glossário de negócios Olá para regido marcação
## <a name="introduction"></a>Introdução
Catálogo de dados do Azure permite a descoberta de fonte de dados, para descobrir e entender as fontes de dados Olá que você precisa de análise de tooperform e toma decisões. Esses recursos tornam o maior impacto de hello quando você pode encontrar e entender o intervalo mais amplo de saudação de fontes de dados disponíveis.

Um recurso do Catálogo de Dados que promove maior compreensão dos dados dos ativos é a marcação. Usando a marcação, você pode associar palavras-chave com um ativo ou uma coluna, o que torna ativo mais fácil de saudação toodiscover via procurando. Marcação também explica mais facilmente contexto hello e a intenção de ativo de saudação.

No entanto, a marcação às vezes pode causar seus próprios problemas. Alguns exemplos de problemas que a marcação pode introduzir são:

* Olá o uso de abreviações de alguns ativos e texto expandido em outros. Essa inconsistência atrapalha descoberta Olá de ativos, mesmo que a intenção de saudação foi tootag ativos de Olá Olá mesma marca.
* Possíveis variações significados, dependendo do contexto. Por exemplo, uma marca chamada *receita* em um cliente o conjunto de dados pode significar a receita por cliente, mas hello mesma marca em um conjunto de dados de vendas trimestral pode significar trimestral receita da empresa hello.  

endereço de toohelp esses e outros desafios semelhantes, catálogo de dados inclui um glossário de negócios.

Usando o Glossário de negócios Olá catálogo de dados, uma organização pode documentar principais termos de negócios e sua definições toocreate um vocabulário comum de negócios. Esse controle permite que a consistência no uso de dados da organização hello. Após a definição de um termo no glossário de negócios hello, ele pode ser atribuído tooa dados ativos no catálogo de saudação. Essa abordagem, *regido marcação*, é Olá a mesma abordagem como marcação.

## <a name="glossary-availability-and-privileges"></a>Disponibilidade de glossário e privilégios
Glossário de negócios Hello está disponível apenas no hello Standard Edition do Data Catalog do Azure. Olá edição gratuita do catálogo de dados não inclui um glossário e não fornece recursos para marcação controlados.

Você pode acessar o Glossário de negócios Olá via Olá **glossário** opção no menu de navegação do portal do catálogo de dados de saudação.  

![Acessando o Glossário de negócios Olá](./media/data-catalog-how-to-business-glossary/01-portal-menu.png)

Os administradores do catálogo de dados e os membros da glossário Olá função de administradores podem criar, editar e excluir termos do glossário de Glossário de negócios hello. Todos os usuários do catálogo de dados podem exibir definições de termos hello e ativos de marca com os termos do glossário.

![Adicionar um novo termo de glossário](./media/data-catalog-how-to-business-glossary/02-new-term.png)

## <a name="creating-glossary-terms"></a>Criar termos do glossário
Os administradores de catálogo de dados e glossário pode criar termos do glossário clicando Olá **novo termo** botão. Cada termo do glossário contém Olá campos a seguir:

* Uma definição de negócios para o termo Olá
* Uma descrição que captura Olá se destina a uso ou regras comerciais para o ativo de saudação ou coluna
* Uma lista de participantes que conhecem hello mais sobre termos de saudação
* termo pai Hello, o que define a hierarquia Olá nas quais Olá é organizado de termo

## <a name="glossary-term-hierarchies"></a>Hierarquias de termos do glossário
Usando o Glossário de negócios Olá catálogo de dados, uma organização pode descrever seu vocabulário de negócios como uma hierarquia de termos e pode criar uma classificação de termos que melhor representa taxonomia seus negócios.

Um termo deve ser exclusivo em um determinado nível de hierarquia. Não são permitidos nomes duplicados. Não há nenhum toohello limitar o número de níveis em uma hierarquia, mas uma hierarquia geralmente é mais facilmente entendida quando há três níveis ou menos.

uso de saudação de hierarquias no glossário de negócios Olá é opcional. Deixar Olá pai termo campo em branco para os termos do glossário cria uma lista de simples (não hierárquico) dos termos no glossário hello.  

## <a name="tagging-assets-with-glossary-terms"></a>Marcar ativos com os termos de glossário
Após a definição de termos do glossário no catálogo Olá, experiência Olá marcação ativos é otimizada toosearch Glossário de saudação que um usuário digita uma marca. portal do catálogo de dados Olá exibe uma lista de correspondência toochoose de termos do glossário de. Se o usuário Olá seleciona um termo do glossário de lista Olá, termo Olá é adicionado toohello ativo como uma tag (também chamada de uma marca de Glossário). Olá usuário também pode optar toocreate uma nova marca digitando um termo que não esteja em Olá Glossário (também chamado de uma marca de usuário).

![Ativo de dados marcado com uma marca de usuário e duas de glossário](./media/data-catalog-how-to-business-glossary/03-tagged-asset.png)

> [!NOTE]
> Marcas de usuário são Olá somente tipo de marca com suporte no hello edição gratuita do catálogo de dados.
>
>

### <a name="hover-behavior-on-tags"></a>Comportamento ao passar o mouse sobre marcas
No portal do catálogo de dados hello, Olá dois tipos de marcas são comportamentos visualmente distintas e presentes em foco diferentes. Quando você focaliza uma marca de usuário, você pode ver o texto de marca hello e usuário hello ou usuários que adicionaram marcas de saudação. Quando você focaliza uma marca glossário, você também ver Olá definição do termo do glossário hello e uma link tooopen Olá business glossário tooview Olá completo definição do termo Olá.

### <a name="search-filters-for-tags"></a>Filtros de pesquisa para marcas
Marcas do usuário e marcas de glossário são pesquisáveis e você pode aplicá-las como filtros em uma pesquisa.

## <a name="summary"></a>Resumo
Usando o Glossário de negócios Olá no Data Catalog do Azure e Olá regido marcação ele permite, você pode identificar, gerenciar e descobrir ativos de dados de maneira consistente. Glossário de negócios Olá pode promover a aprendizagem de vocabulário de negócios Olá por membros da organização. Glossário do Hello também dá suporte a capturar metadados significativo, o que simplifica a compreensão e a descoberta de ativo.

## <a name="next-steps"></a>Próximas etapas
* [Documentação da API REST para operações de glossário de negócios](https://msdn.microsoft.com/library/mt708855.aspx)
