---
title: Tabela de API da aaaIntroduction tooAzure Cosmos banco de dados | Microsoft Docs
description: "Saiba como você pode usar o banco de dados do Azure Cosmos toostore e grandes volumes de consulta de dados de chave-valor com o uso de baixa latência Olá populares OSS MongoDB APIs."
services: cosmos-db
author: bhanupr
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/25/2017
ms.author: arramac
ms.openlocfilehash: 4c5678898a772808f4bcd1465a23d436b0f8fc0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-table-api"></a>Introdução tooAzure Cosmos DB: API de tabela

O [Azure Cosmos DB](introduction.md) é o serviço multimodelo de banco de dados da Microsoft, distribuído globalmente, para aplicativos críticos. Banco de dados do Azure Cosmos fornece [distribuição global turnkey](distribute-data-globally.md), [dimensionamento Elástico de taxa de transferência e armazenamento](partition-data.md) latências de milissegundo em todo o mundo, dígito no percentual de 99th hello, [cinco níveis de consistência bem definidos](consistency-levels.md)e a garantia de alta disponibilidade, apoiada por [SLAs do setor](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Banco de dados do Azure Cosmos [indexa automaticamente os dados](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sem exigir que você toodeal com o gerenciamento de esquema e de índice. Ele tem vários modelos e suporta modelos de dados de colunas, gráficos, valores-chave e documentos. 

![API de Armazenamento de Tabelas do Azure e BD Cosmos do Azure](./media/table-introduction/premium-tables.png) 

Banco de dados do Azure Cosmos fornece Olá tabela API (visualização) para aplicativos que precisam de um repositório de chave-valor com esquema flexível, desempenho previsível, distribuição global e alta taxa de transferência. Olá API tabela fornece Olá mesma funcionalidade de armazenamento de tabela do Azure, mas aproveita os benefícios de saudação do mecanismo de banco de dados do Azure Cosmos hello. 

Você pode continuar toouse armazenamento de tabela do Azure para tabelas com armazenamento de alta e reduzir os requisitos de taxa de transferência. Banco de dados do Azure Cosmos apresenta suporte para tabelas com otimização de armazenamento em uma atualização futura e tabela de Azure existentes e novas contas de armazenamento será atualizado tooAzure Cosmos DB.

## <a name="premium-and-standard-table-apis"></a>APIs de tabela padrão e premium
Se você usar o armazenamento de tabela do Azure no momento, você ganha Olá benefícios a seguir ao mover a visualização de "tabela premium" tooAzure Cosmos DB:

|  | Armazenamento de Tabelas do Azure | BD Cosmos do Azure: Armazenamento de Tabelas (versão prévia) |
| --- | --- | --- |
| Latência | Rápido, mas não há limites superiores na latência | Dígito milissegundos de latência para leituras e gravações, feito com < lê de latência de 10 ms e < gravações de latência de 15 ms percentil 99th hello, em qualquer escala, em qualquer lugar no Olá, mundo |
| Taxa de transferência | Modelo de taxa de transferência altamente escalonável, mas não dedicado. As tabelas têm um limite de escalabilidade de 20.000 operações/s | Altamente escalonável com [taxa de transferência reservada dedicada por tabela](request-units.md), que é respaldada por SLAs. As contas não têm nenhum limite superior na taxa de transferência e dão suporte para >10 milhões de operações/s por tabela |
| Distribuição Global | Região única com uma região secundária legível opcional para alta disponibilidade. Você não pode iniciar o failover | [Distribuição global turnkey](distribute-data-globally.md) de um too30 + regiões, suporte para [failovers automáticos e manuais](regional-failover.md) a qualquer momento, em qualquer lugar no Olá, mundo |
| Indexação | Somente índice primário em PartitionKey e RowKey. Nenhum índice secundário | Indexação automática e completa em todas as propriedades, não há gerenciamento de índice |
| Consultar | A execução de consulta usa o índice para chave primária. Caso contrário, realiza a verificação. | As consultas podem aproveitar a indexação automática em propriedades para tempos rápidos de consulta. O mecanismo do banco de dados do BD Cosmos do Azure é capaz de dar suporte agregações, geoespacial e classificação. |
| Consistência | Forte na região primária, eventual na região secundária | [Cinco níveis de consistência bem definidos](consistency-levels.md) tootrade disponibilidade, latência, taxa de transferência e consistência com base em suas necessidades de aplicativo |
| Preços | Otimização de armazenamento  | Otimização de taxa de transferência |
| SLAs | 99,9% de disponibilidade | disponibilidade de 99,99% em uma única região e capacidade tooadd mais regiões para maior disponibilidade. [SLAs abrangentes líderes do setor](https://azure.microsoft.com/support/legal/sla/cosmos-db/) em disponibilidade geral |

## <a name="how-tooget-started"></a>A inicialização de tooget

Criar uma conta de banco de dados do Azure Cosmos Olá [portal do Azure](https://portal.azure.com)e começar a usar nossos [início rápido para a API de tabela usando o .NET](create-table-dotnet.md). 

## <a name="next-steps"></a>Próximas etapas

Aqui estão alguns tooget ponteiros é iniciado:
* [Criar um aplicativo .NET usando Olá API de tabela](create-table-dotnet.md)
* [Desenvolver com hello API de tabela no .NET](tutorial-develop-table-dotnet.md)
* [Consultar dados de tabela usando Olá API de tabela](tutorial-query-table.md)
* [Como a distribuição global usando o banco de dados do Azure Cosmos toosetup Olá API de tabela](tutorial-global-distribution-table.md)
* [SDK da API de Tabela do Azure Cosmos DB para .NET](table-sdk-dotnet.md)
