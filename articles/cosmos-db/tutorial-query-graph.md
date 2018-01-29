---
title: Como consultar dados do grafo no Azure Cosmos DB? | Microsoft Docs
description: Aprenda a consultar dados do grafo no Azure Cosmos DB
services: cosmos-db
documentationcenter: 
author: luisbosquez
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 01/02/2018
ms.author: lbosq
ms.custom: mvc
ms.openlocfilehash: 5a635abfa9fa10cd8c8498e3c95a17af997cea3e
ms.sourcegitcommit: 9ea2edae5dbb4a104322135bef957ba6e9aeecde
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/03/2018
---
# <a name="azure-cosmos-db-how-to-query-with-the-graph-api"></a>Azure Cosmos DB: Como consultar com a API do Graph?

A [API do Graph](graph-introduction.md) do Azure Cosmos DB também é compatível com consultas do [Gremlin](https://github.com/tinkerpop/gremlin/wiki). Este artigo fornece exemplos de documentos e consultas para você começar. Uma referência detalhada do Gremlin é fornecida no artigo [Suporte a Gremlin](gremlin-support.md).

Este artigo aborda as seguintes tarefas: 

> [!div class="checklist"]
> * Consultar dados com o Gremlin

## <a name="prerequisites"></a>pré-requisitos

Para essas consultas funcionarem, você deve ter uma conta do Azure Cosmos DB e ter dados de grafo no contêiner. Não tenho nenhum deles? Complete o [Guia de início rápido de cinco minutos](create-graph-dotnet.md) ou o [tutorial de desenvolvedor](tutorial-query-graph.md) para criar uma conta e preencher seu banco de dados. Você pode executar as seguintes consultas usando a [Biblioteca de grafos do .NET do Azure Cosmos DB](graph-sdk-dotnet.md), [Console do Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) ou o seu driver favorito do Gremlin.

## <a name="count-vertices-in-the-graph"></a>Contagem de vértices no grafo

O trecho a seguir mostra como contar o número de vértices no grafo:

```
g.V().count()
```

## <a name="filters"></a>Filtros

Execute filtros usando as etapas `has` e `hasLabel` do Gremlin e combine-as usando `and`, `or` e `not` para compilar filtros mais complexos. O Azure Cosmos DB fornece indexação independente do esquema de todas as propriedades em seus vértices e graus para consultas rápidas:

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a>Projeção

Você pode projetar certas propriedades nos resultados da consulta usando a etapa `values`:

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a>Localizar os vértices e bordas relacionadas

Até agora, só vimos operadores de consulta que funcionam em qualquer banco de dados. Os grafo são rápidos e eficientes para operações de passagem quando você precisa navegar até os vértices e bordas relacionadas. Vamos encontrar todos os amigos de Thomas. Fazemos isso usando a etapa `outE` do Gremlin para localizar todos as bordas externas de Thomas, depois passamos para os vértices internos dessas bordas usando a etapa `inV` do Gremlin:

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

A próxima consulta executa dois saltos para localizar todos os "amigos dos amigos" de Thomas, chamando `outE` e `inV` duas vezes. 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

Você pode criar consultas mais complexas e implementar uma lógica avançada de passagem de grafo usando o Gremlin, incluindo a combinação de expressões de filtro, executando o loop usando a etapa `loop` e implementando a navegação condicional usando a etapa `choose`. Saiba mais sobre o que você pode fazer com o [Suporte do Gremlin](gremlin-support.md)!

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você fez o seguinte:

> [!div class="checklist"]
> * Aprendeu a consultar usando o Graph 

Agora você pode prosseguir para o próximo tutorial e aprender a distribuir seus dados globalmente.

> [!div class="nextstepaction"]
> [Distribuir os dados globalmente](tutorial-global-distribution-sql-api.md)
