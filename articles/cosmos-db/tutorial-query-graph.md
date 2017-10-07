---
title: "dados do gráfico aaaHow tooquery no banco de dados do Azure Cosmos? | Microsoft Docs"
description: "Saiba mais dados do gráfico tooquery no banco de dados do Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: fdde881edd6c488e2fea51e5c9665e1d736009fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a>Cosmos do Azure DB: Como tooquery com hello Graph API (visualização)?

Olá banco de dados do Azure Cosmos [API do Graph](graph-introduction.md) (visualização) oferece suporte a [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) consultas. Este artigo fornece documentos de exemplo e consultas tooget que é iniciado. Uma referência detalhada de Gremlin é fornecida no hello [suporte Gremlin](gremlin-support.md) artigo.

Este artigo aborda Olá tarefas a seguir: 

> [!div class="checklist"]
> * Consultar dados com o Gremlin

## <a name="prerequisites"></a>Pré-requisitos

Para toowork essas consultas, você deve ter uma conta de banco de dados do Azure Cosmos e ter dados de gráfico no contêiner de saudação. Não tenho nenhum deles? Olá completa [início rápido de 5 minutos](create-graph-dotnet.md) ou hello [tutorial de desenvolvedor](tutorial-query-graph.md) toocreate uma conta e preencher o banco de dados. Você pode executar Olá consultas usando Olá a seguir [biblioteca gráfica do Azure Cosmos DB .NET](graph-sdk-dotnet.md), [console Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), ou o driver Gremlin favorito.

## <a name="count-vertices-in-hello-graph"></a>Contagem de vértices no gráfico de saudação

saudação de trecho de código a seguir mostra como toocount Olá número de vértices no gráfico de saudação:

```
g.V().count()
```

## <a name="filters"></a>Filtros

Você pode executar filtros usando do Gremlin `has` e `hasLabel` etapas e combiná-los usando `and`, `or`, e `not` toobuild os filtros mais complexos. O Azure Cosmos DB fornece indexação independente do esquema de todas as propriedades em seus vértices e graus para consultas rápidas:

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a>Projeção

Você pode projetar determinadas propriedades em resultados da consulta hello usando Olá `values` etapa:

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a>Localizar os vértices e bordas relacionadas

Até agora, só vimos operadores de consulta que funcionam em qualquer banco de dados. Gráficos são rápidos e eficientes para operações de passagem quando você precisa toonavigate toorelated bordas e vértices. Vamos encontrar todos os amigos de Thomas. Podemos fazer isso por meio do Gremlin `outE` etapa toofind Olá todas as out-bordas de Thomas, em seguida, passar toohello nos vértices das bordas usando do Gremlin `inV` etapa:

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

executa a consulta seguinte Olá toofind de dois saltos todos "amigos Thomas intitulado dos amigos", chamando `outE` e `inV` duas vezes. 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

Você pode criar consultas mais complexas e implementar a lógica de passagem de gráfico avançado usando Gremlin, incluindo filtro combinação expressões, executar um loop usando Olá `loop` etapa e implementação navegação condicional usando Olá `choose` etapa. Saiba mais sobre o que você pode fazer com o [Suporte do Gremlin](gremlin-support.md)!

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você fez a seguir hello:

> [!div class="checklist"]
> * Aprendeu como tooquery usando o Graph 

Você pode continuar toolearn tutorial do próximo toohello como toodistribute seus dados globalmente.

> [!div class="nextstepaction"]
> [Distribuir os dados globalmente](tutorial-global-distribution-documentdb.md)