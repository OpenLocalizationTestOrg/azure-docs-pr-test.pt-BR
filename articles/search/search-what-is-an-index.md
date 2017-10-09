---
title: "aaaCreate um índice de pesquisa do Azure | Microsoft Azure | Serviço de pesquisa de nuvem hospedada"
description: "O que é um índice na Pesquisa do Azure e como é usado?"
services: search
documentationcenter: 
author: ashmaka
ms.assetid: a395e166-bf2e-4fca-8bfc-116a46c5f7b1
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: c01cc654ff91427c8f1569b2f5b060a0a0f044c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index"></a>Criar um índice de pesquisa do Azure
> [!div class="op_single_selector"]
> * [Visão geral](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

## <a name="what-is-an-index"></a>O que é um índice?
Um *índice* é o repositório persistente de *documentos* e outras construções usados por um serviço do Azure Search. Um documento é um dado pesquisável da unidade no índice. Por exemplo, uma loja de comércio eletrônico pode ter um documento para cada item vendido, uma agência de notícias pode ter um documento para cada artigo etc. Equivalentes de familiares de banco de dados de toomore esses conceitos de mapeamento: um *índice* é conceitualmente semelhante tooa *tabela*, e *documentos* são praticamente equivalentes muito*linhas* em uma tabela.

Quando você adiciona/carregar documentos e enviar consultas de pesquisa tooAzure pesquisa, envie o índice específico de tooa solicitações em seu serviço de pesquisa.

## <a name="field-types-and-attributes-in-an-azure-search-index"></a>Tipos de campo e atributos em um índice da Pesquisa do Azure
Como definir o esquema, você deve especificar Olá nome, tipo e atributos de cada campo no índice. tipo de campo Olá classifica os dados de saudação que são armazenados no campo. Atributos são definidos em campos individuais toospecify como campo de saudação é usado. Olá tabelas a seguir enumerar tipos de saudação e atributos que você pode especificar.

### <a name="field-types"></a>Tipos de campo
| Tipo | Descrição |
| --- | --- |
| *Edm.String* |O texto que opcionalmente pode ser indexado para a pesquisa de texto completo (separação de palavras, derivação etc). |
| *Collection(Edm.String)* |Uma lista de cadeias de caracteres que opcionalmente podem ser indexadas para a pesquisa de texto completo. Não há nenhum limite teórico no número de saudação de itens em uma coleção, mas o limite superior de 16 MB de saudação no tamanho da carga se aplica a toocollections. |
| *Edm.Boolean* |Contém valores true/false. |
| *Edm.Int32* |Valores inteiros de 32 bits. |
| *Edm.Int64* |Valores inteiros de 64 bits. |
| *Edm.Double* |Dados numéricos de dupla precisão. |
| *Edm.DateTimeOffset* |Os valores de hora representados no formato Olá OData V4 de data (por exemplo, `yyyy-MM-ddTHH:mm:ss.fffZ` ou `yyyy-MM-ddTHH:mm:ss.fff[+/-]HH:mm`). |
| *Edm.GeographyPoint* |Um ponto que representa uma localização geográfica em todo mundo de saudação. |

Você pode encontrar informações mais detalhadas sobre os [tipos de dados com suporte](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) do Azure Search.

### <a name="field-attributes"></a>Atributos do campo
| Atributo | Descrição |
| --- | --- |
| *Chave* |Uma cadeia de caracteres que fornece Olá a ID exclusiva de cada documento, usado para pesquisar documento. Todos os índices devem ter uma chave. Somente um campo pode ser chave hello e seu tipo deve ser definido como tooEdm.String. |
| *Recuperável* |Especifica se um campo pode ser retornado em um resultado da pesquisa. |
| *Filtrável* |Permite Olá toobe de campo usada em consultas de filtro. |
| *Classificável* |Permite que uma consulta de resultados da pesquisa toosort usando este campo. |
| *Com faceta* |Permite que um toobe de campo usada em uma [navegação facetada](search-faceted-navigation.md) estrutura para a filtragem automática direcionado do usuário. Normalmente os campos que contêm valores repetitivos que você pode usar toogroup juntos de vários documentos (por exemplo, vários documentos que se enquadram em uma única marca ou a categoria de serviço) funcionam melhor como facetas. |
| *Pesquisável* |Marcas Olá campo como pesquisa de texto completo. |

Você pode encontrar informações mais detalhadas sobre os [atributos de índice](https://docs.microsoft.com/rest/api/searchservice/Create-Index) do Azure Search.

## <a name="guidance-for-defining-an-index-schema"></a>Diretrizes para definir um esquema de índice
Como você projeta seu índice, reserve algum tempo no hello toothink fase por meio de cada decisão de planejamento. É importante que você mantenha suas necessidades de negócios e experiência de usuário pesquisa em mente ao criar o índice de cada campo deve ser atribuída a saudação [atributos adequados](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Alterar um índice depois de ser implantado envolve a recriação e recarregar dados hello.

Se os requisitos do armazenamento de dados mudarem com o tempo, você poderá aumentar ou diminuir a capacidade adicionando ou removendo as partições. Para obter detalhes, confira [Gerenciar o serviço Search no Azure](search-manage.md) ou [Limites de serviço](search-limits-quotas-capacity.md).

