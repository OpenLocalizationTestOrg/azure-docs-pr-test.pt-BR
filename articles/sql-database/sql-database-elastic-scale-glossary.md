---
title: "Glossário de ferramentas de banco de dados aaaElastic | Microsoft Docs"
description: "Explicação dos termos usados para as ferramentas de banco de dados elástico"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: d6573aad9a097e07135b0a64d1dafec19bb8cc7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-tools-glossary"></a>Glossário de ferramentas do banco de dados elástico
Olá termos a seguir são definidos para Olá [ferramentas de banco de dados Elástico](sql-database-elastic-scale-introduction.md), um recurso do banco de dados do SQL Azure. ferramentas Hello são usada toomanage [mapas de fragmento](sql-database-elastic-scale-shard-map-management.md)e incluem hello [biblioteca de cliente](sql-database-elastic-database-client-library.md), Olá [ferramenta de mesclagem de divisão](sql-database-elastic-scale-overview-split-and-merge.md), [pools Elásticos](sql-database-elastic-pool.md), e [consultas](sql-database-elastic-query-overview.md). 

Esses termos são usados em [adicionando um fragmento usando as ferramentas de banco de dados Elástico](sql-database-elastic-scale-add-a-shard.md) e [usando problemas de mapa de fragmento Olá RecoveryManager classe toofix](sql-database-elastic-database-recovery-manager.md).

![Termos de escala elástica][1]

**Banco de dados**: um Banco de Dados SQL do Azure. 

**Roteamento dependente de dados**: Olá funcionalidade que permite que um fragmento de tooa tooconnect aplicativo recebe uma chave de fragmentação específico. Consulte [Roteamento dependente de dados](sql-database-elastic-scale-data-dependent-routing.md). Comparar muito**[vários fragmentos consulta](sql-database-elastic-scale-multishard-querying.md)**.

**Mapa do fragmento global**: Olá mapa entre as chaves de fragmentação e seus respectivos fragmentos em um **conjunto de fragmentos**. mapa do fragmento global de saudação é armazenado no hello **Gerenciador do mapa de fragmentos**. Comparar muito**mapa do fragmento local**.

**Mapa de fragmentos de lista**: um mapa de fragmentos no qual as chaves de fragmentação são mapeadas individualmente. Comparar muito**mapa do fragmento intervalo**.   

**Mapa do fragmento local**: armazenado em um fragmento, mapa de fragmento local Olá contém mapeamentos de saudação shardlets que residem em um fragmento de saudação.

**Consulta de vários fragmento**: Olá capacidade tooissue uma consulta em vários fragmentos; os conjuntos de resultados são retornados usando UNION ALL semânticas (também conhecido como "consulta de fan-out"). Comparar muito**roteamento dependente de dados**.

**Multilocatário** e **Locatário único**: mostra um banco de dados com locatário único e um banco de dados multilocatário:

![Bancos de dados de único locatário e multilocatário](./media/sql-database-elastic-scale-glossary/multi-single-simple.png)

Esta é uma representação de bancos de dados de único locatário e multilocatário **fragmentados** . 

![Bancos de dados de único locatário e multilocatário](./media/sql-database-elastic-scale-glossary/shards-single-multi.png)

**Mapa do fragmento intervalo**: um mapa do fragmento que Olá estratégia de distribuição do fragmento é baseada em vários intervalos de valores contíguos. 

**Tabelas de referência**: tabelas que não são fragmentadas, mas replicadas nos fragmentos. Por exemplo, códigos postais podem ser armazenados em uma tabela de referência. 

**Fragmento**: um banco de dados SQL do Azure que armazena dados de um conjunto de dados fragmentados. 

**Elasticidade de fragmento**: Olá capacidade tooperform **escalonamento horizontal** e **dimensionamento vertical**.

**Tabelas fragmentadas**: tabelas que são fragmentadas, ou seja, cujos dados são distribuídos por meio de fragmentos com base em seus valores de chave de fragmentação. 

**Chave de fragmentação**: um valor de coluna que determina como os dados são distribuídos nos fragmentos. Olá tipo de valor pode ser um dos seguintes Olá: **int**, **bigint**, **varbinary**, ou **uniqueidentifier**. 

**Conjunto de fragmentos**: Olá coleção de fragmentos são toohello atribuído mesmo mapa do fragmento no Gerenciador do mapa de fragmentos hello.  

**Shardlet**: todos os dados de saudação associados a um único valor de uma chave de fragmentação em um fragmento. Um shardlet é a menor unidade Olá de movimentação de dados possível quando redistribuindo tabelas fragmentadas. 

**Mapa do fragmento**: Olá conjunto de mapeamentos entre as chaves de fragmentação e seus respectivos fragmentos.

**Gerenciador do mapa de fragmentos**: um repositório de dados e o objeto de gerenciamento que contém mapas de fragmento hello, locais de fragmento e mapeamentos para um ou mais conjuntos de fragmento.

![Mapeamentos][2]

## <a name="verbs"></a>Verbos
**Escalonamento horizontal**: ato de saudação de scaling out (ou em) um conjunto de fragmentos, adicionando ou removendo o mapa do fragmento tooa fragmentos, conforme mostrado abaixo.

![Dimensionamento horizontal e vertical][3]

**Mesclar**: ato de saudação de mover shardlets de fragmento de tooone dois fragmentos e atualizando o mapa do fragmento Olá adequadamente.

**Mover Shardlets**: ato de saudação de movimentação de um fragmento diferente de tooa único shardlet. 

**Fragmento**: ato de saudação de particionamento horizontal de forma idêntica dados estruturados em vários bancos de dados com base em uma chave de fragmentação.

**Divisão**: act Olá mover vários shardlets do fragmento (normalmente novo) de tooanother um fragmento. Uma chave de fragmentação é fornecida pelo usuário Olá Olá ponto de divisão.

**Escala vertical**: ato de saudação de dimensionamento para cima (ou para baixo) Olá nível de desempenho de um fragmento individual. Por exemplo, alterar um fragmento de tooPremium padrão (o que resulta em mais recursos de computação). 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-glossary/glossary.png
[2]: ./media/sql-database-elastic-scale-glossary/mappings.png
[3]: ./media/sql-database-elastic-scale-glossary/h_versus_vert.png

