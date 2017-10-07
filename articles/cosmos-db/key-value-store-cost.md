---
title: "aaaAzure DB Cosmos como um armazenamento de valor de chave – visão geral de custo | Microsoft Docs"
description: Saiba mais sobre o custo de usando o banco de dados do Azure Cosmos como um armazenamento de valor de chave baixo hello.
keywords: "repositório de valores de chave"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: 
documentationcenter: 
ms.assetid: 7f765c17-8549-4509-9475-46394fc3a218
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: mimig
ms.openlocfilehash: de7207760a8e1fca0e30f951109748835dabf4a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-as-a-key-value-store--cost-overview"></a>Azure Cosmos DB como um repositório de valores de chave – Visão geral do custo

O Azure Cosmos DB é um serviço de multimodelo de banco de dados distribuído globalmente e totalmente gerenciado para a criação fácil de aplicativos altamente disponíveis de grande escala. Por padrão, o banco de dados do Azure Cosmos indexa automaticamente todos os dados de saudação com eficiência consome. Isso permite consultas [SQL](documentdb-sql-query.md) (e [JavaScript](programming.md)) rápidas e consistentes em qualquer tipo de dados. 

Este artigo descreve o custo de saudação do banco de dados do Azure Cosmos para gravação simple e operações de leitura quando ele é usado como um repositório de chave/valor. Operações de gravação incluem inserções, substituições, exclusões e upserts de documentos. Além de garantir a alta disponibilidade de 99,99%, a garantia de ofertas de banco de dados do Azure Cosmos < latência de 10 ms para leituras e < latência de 15 ms para hello (indexada) respectivamente, grava no percentual 99th hello. 

## <a name="why-we-use-request-units-rus"></a>Por que usamos RUs (Unidades de Solicitação)

Desempenho de banco de dados do Cosmos do Azure é com base na quantidade de saudação do provisionado [unidades de solicitação](request-units.md) (RU) para a partição de saudação. saudação de provisionamento está em uma granularidade de segundo e é adquirido em RUs/s e RUs/min ([toobe não confundido com hello cobrança por hora](https://azure.microsoft.com/pricing/details/cosmos-db/)). RUs devem ser consideradas como uma moeda que simplifica o provisionamento de saudação de taxa de transferência necessária para o aplicativo hello. Os clientes não têm toothink de diferenciar entre leitura e gravação a unidades de capacidade. modelo de única moeda de saudação do RUs cria eficiências de capacidade de saudação provisionada tooshare entre leituras e gravações. Esse modelo de capacidade provisionada permite Olá serviço tooprovide uma taxa de transferência consistente e previsível, a garantia de baixa latência e alta disponibilidade. Finalmente, usamos a taxa de transferência de toomodel RU, mas cada RU provisionado também tem uma quantidade definida de recursos (memória, Core). RU/s não é apenas o IOPS.

Como um sistema de banco de dados distribuído globalmente, Cosmos DB é Olá somente o serviço do Azure que fornece um SLA na latência, a taxa de transferência e a consistência na disponibilidade de toohigh de adição. taxa de transferência de saudação que provisionar é aplicado tooeach das regiões Olá associado à sua conta de banco de dados do banco de dados do Cosmos. Para leituras, o banco de dados do Cosmos oferece vários bem definido [níveis de consistência](consistency-levels.md) para você toochoose do. 

Olá tabela a seguir mostra Olá inúmeros RUs tooperform necessário leitura e gravação das transações com base no tamanho do documento de 1KB e 100KBs.

|Tamanho do Item|1 Leitura|1 Gravação|
|-------------|------|-------|
|1 KB|1 RU|5 RUs|
|100 KB|10 RUs|50 RUs|

## <a name="cost-of-reads-and-writes"></a>Custo de leituras e gravações

Se você provisionar 1.000 RU/s, isso equivale too3.6m RU/hora e custa US $0,08 por hora de saudação (em hello dos EUA e Europa). Para um documento com 1KB, isso significa que você pode consumir 3,6 m de leituras ou 0,72 m de gravações (3,6m RU/5) usando sua taxa de transferência provisionada. Toomillion normalizado leituras e gravações, Olá custo seria $0.022 /m leituras (US $0,08 / 3,6) e grava $0.111/ m (US $0,08 / 0.72). Olá custo por milhões torna-se mínimo conforme mostrado na tabela de saudação abaixo.

|Tamanho do Item|1m de Leitura|1m de Gravação|
|-------------|-------|--------|
|1 KB|$ 0,022|$ 0,111|
|100 KB|$ 0,222|$ 1,111|


Maioria dos blob básico hello ou encargos de serviços de repositórios de objeto $0,40 por milhão de transação de leitura e US $5 por transação de gravação milhões. Se usado de maneira ideal, Cosmos banco de dados pode ser o too98% mais barato do que essas outras soluções (para transações de 1KB).

## <a name="next-steps"></a>Próximas etapas

Fique atento a novos artigos sobre como otimizar o provisionamento de recursos do Azure Cosmos DB. Em Olá enquanto isso, sinta-se livre toouse nosso [Calculadora RU](https://www.documentdb.com/capacityplanner).

