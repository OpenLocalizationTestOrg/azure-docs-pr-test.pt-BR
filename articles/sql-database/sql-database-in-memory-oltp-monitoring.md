---
title: "armazenamento de na memória XTP aaaMonitor | Microsoft Docs"
description: "Estimar e monitorar o uso do armazenamento na memória XTP, capacidade; resolver o erro de capacidade 41823"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: fcb17bd8e9ebef4862d4b55bf5a79b45b9419fca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-in-memory-oltp-storage"></a>Monitorar o armazenamento OLTP na memória
Ao usar o [In-Memory OLTP](sql-database-in-memory.md), os dados em tabelas com otimização de memória e as variáveis de tabela residem no armazenamento OLTP in-memory. Cada camada de serviço Premium tem um tamanho de armazenamento máximo do OLTP na memória, que está documentado na Olá [artigo de camadas de serviço de banco de dados do SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels). Quando esse limite for excedido, as operações insert e update poderão começar a falhar (com o erro 41823). Nesse momento você precisa de memória de tooreclaim tooeither excluir dados ou atualizar a camada de desempenho de saudação do banco de dados.

## <a name="determine-whether-data-will-fit-within-hello-in-memory-storage-cap"></a>Determinar se dados serão ajustadas dentro do limite de armazenamento na memória Olá
Determinar o limite de armazenamento Olá: consulte Olá [artigo de camadas de serviço de banco de dados SQL](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) para limites de armazenamento Olá das diferentes camadas de serviço Premium Olá.

Estimar memória requisitos para uma tabela com otimização de memória funciona Olá mesmo como para o SQL Server como ele faz no banco de dados do SQL Azure. Assumir tooreview de alguns minutos esse tópico [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).

Observe que a tabela hello e linhas de variável de tabela, bem como índices, contam para o tamanho de dados de usuário max hello. Além disso, ALTER TABLE precisa toocreate suficiente espaço uma nova versão da tabela inteira hello e seus índices.

## <a name="monitoring-and-alerting"></a>Monitoramento e alertas
Você pode monitorar o uso de armazenamento na memória como uma porcentagem da saudação [limite de armazenamento para o nível de desempenho](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) em hello Azure [portal](https://portal.azure.com/): 

* Na folha de banco de dados Olá, localize a caixa de utilização de recurso hello e clique em Editar.
* Em seguida, selecione a métrica de saudação `In-Memory OLTP Storage percentage`.
* tooadd um alerta, clique na folha da métrica de Olá Olá utilização de recursos caixa tooopen, clique em Adicionar alerta.

Ou use Olá utilização de armazenamento na memória consulta tooshow Olá a seguir:

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a>Corrigir situações de memória insuficiente - Erro 41823
A insuficiência de memória resulta na falha das operações INSERT, UPDATE e CREATE com a mensagem de erro 41823.

Mensagem de erro 41823 indica que as tabelas com otimização de memória hello e variáveis de tabela excedeu o tamanho máximo de saudação.

tooresolve esse erro, ou:

* Excluir dados de tabelas com otimização de memória hello, tootraditional potencialmente descarregamento de dados hello, tabelas baseadas em disco. ou,
* Atualizar Olá tooone de nível de serviço com armazenamento suficiente de memória para dados de saudação é necessário tookeep nas tabelas com otimização de memória.

## <a name="next-steps"></a>Próximas etapas
Para obter diretrizes sobre monitoramento, consulte [Monitoramento de Banco de Dados SQL do Azure usando exibições de gerenciamento dinâmico](sql-database-monitoring-with-dmvs.md).
