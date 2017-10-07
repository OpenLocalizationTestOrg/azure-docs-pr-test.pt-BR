---
title: "Banco de Dados SQL: O que é um DTU? | Microsoft Docs"
description: "Noções básicas sobre o que uma unidade de transação do Banco de Dados SQL."
keywords: "opções de banco de dados, desempenho do banco de dados"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: CarlRabeler
ms.assetid: 89e3e9ce-2eeb-4949-b40f-6fc3bf520538
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 04/13/2017
ms.author: carlrab
ms.openlocfilehash: ba1fe580b32826259edaf6c8dc124faaf5b3d234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-database-transaction-units-dtus-and-elastic-database-transaction-units-edtus"></a>Explicação de DTUs (Unidades de transação de banco de dados) e eDTUs (Unidades de transação de banco de dados elástico)
Este artigo explica como unidades de transação do banco de dados (DTUs) e unidades de transação de banco de dados Elástico (eDTUs) e o que acontece quando você atinge Olá máximo de DTUs ou eDTUs.  

## <a name="what-are-database-transaction-units-dtus"></a>O que são DTUs (Unidades de transação do banco de dados)
Para um único banco de dados do SQL Azure em um nível de desempenho específicos dentro de um [camada de serviço](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels), Microsoft garante um certo nível de recursos do banco de dados (independente de qualquer outro banco de dados na nuvem do Azure de saudação) e fornecendo um previsível nível de desempenho. Essa quantidade de recursos é calculada como um número de unidades de transação do banco de dados ou DTUs e é uma medida combinada de CPU, memória, E/S (E/S de dados e log de transações). taxa de saudação entre esses recursos originalmente foi determinada por uma [carga de trabalho OLTP benchmark](sql-database-benchmark-overview.md) projetado toobe típico de cargas de trabalho OLTP reais. Quando sua carga de trabalho excede a quantidade de saudação de qualquer um desses recursos, a taxa de transferência está limitado - resultando em desempenho mais lento e tempos limite. recursos de saudação usados pela sua carga de trabalho não afetem Olá recursos tooother disponíveis bancos de dados SQL Olá nuvem do Azure e o recurso de saudação usado por outras cargas de trabalho não afeta o banco de dados SQL tooyour disponíveis de recursos de saudação.

![caixa delimitadora](./media/sql-database-what-is-a-dtu/bounding-box.png)

DTUs são mais úteis para a quantidade relativa do hello compreensão de recursos entre bancos de dados SQL Azure em diferentes níveis de desempenho e as camadas de serviço. Por exemplo, dobrar Olá DTUs aumentando o nível de desempenho de saudação do banco de dados equivale toodoubling conjunto de saudação do banco de dados do recurso toothat disponíveis. Por exemplo, um banco de dados Premium P11 com 1.750 DTUs fornece 350x mais capacidade de computação DTU que um banco de dados básico com 5 DTUs.  

toogain mais aprofundado sobre consumo de recursos (DTU) de saudação da carga de trabalho, use [análise de desempenho de consulta do banco de dados de SQL do Azure](sql-database-query-performance.md) para:

- Identificar as principais consultas de saudação por contagem de duração/CPU/execução potencialmente pode ser ajustada para melhorar o desempenho. Por exemplo, uma consulta com uso intensivo de e/s pode se beneficiar do uso de saudação do [técnicas de otimização de memória](sql-database-in-memory.md) toomake melhor o uso de memória disponível de saudação em determinados níveis de serviço da camada e o desempenho.
- Fazer drill down nos detalhes de saudação de uma consulta, exibir seu texto e o histórico de utilização de recursos.
- Acesse recomendações de ajuste de desempenho que mostram as ações executadas pelo [Assistente do Banco de Dados SQL do Azure](sql-database-advisor.md).

Você pode [alterar as camadas de serviço](sql-database-service-tiers.md) a qualquer momento com aplicativos do tempo de inatividade mínimo tooyour (geralmente média em quatro segundos). Para muitas empresas e aplicativos, sendo toocreate capaz de bancos de dados e desempenho para cima ou para baixo sob demanda de discagem é suficiente, principalmente se os padrões de uso são relativamente previsíveis. Mas se você tiver os padrões de uso imprevisíveis, ele pode tornar os custos de disco rígido toomanage e seu modelo de negócios. Para este cenário, você pode usar um pool Elástico com um determinado número de eDTUs que são compartilhadas entre várias banco de dados no pool de saudação.

![Introdução tooSQL banco de dados: único DTUs de banco de dados da camada e nível](./media/sql-database-what-is-a-dtu/single_db_dtus.png)

## <a name="what-are-elastic-database-transaction-units-edtus"></a>O que são eDTUs (Unidades de transação de banco de dados elástico)
Em vez de fornecer um conjunto dedicado de recursos (DTUs) tooa banco de dados SQL que está sempre disponível independentemente de se não necessário, você pode colocar bancos de dados em um [pool Elástico](sql-database-elastic-pool.md) em um servidor de banco de dados SQL que compartilha um pool de recursos entre os banco de dados. recursos de saudação compartilhado em um pool Elástico medido por Elástico unidades de transação do banco de dados ou eDTUs. Pools Elásticos fornecem uma solução econômica simples toomanage metas de desempenho de saudação para vários bancos de dados com diferentes amplamente e padrões de uso imprevisível. Em um pool Elástico, você pode garantir que não há um banco de dados usa todos os recursos de saudação no pool de saudação e também que uma quantidade mínima de recursos é sempre o banco de dados tooa disponível em um pool Elástico. Confira [pools elásticos](sql-database-elastic-pool.md) para obter mais informações.

![Introdução tooSQL banco de dados: eDTUs por camada e nível](./media/sql-database-what-is-a-dtu/sqldb_elastic_pools.png)

Um pool é fornecido com um número definido de eDTUs por um preço definido. Em pool Elástico de hello, bancos de dados individuais recebem Olá flexibilidade tooauto escala dentro dos limites de saudação configurado. Sob carga pesada, um banco de dados pode consumir mais demanda de toomeet eDTUs enquanto bancos de dados sob carga leve consumam menos, bancos de dados em nenhuma carga não consomem nenhum eDTUs de ponto de toohello. Provisionando recursos para o pool inteiro Olá, em vez de por banco de dados, as tarefas de gerenciamento são simplificadas e têm um orçamento previsível para o pool de saudação.

EDTUs adicionais podem ser adicionados tooan o pool existente sem tempo de inatividade do banco de dados e sem nenhum impacto em bancos de dados Olá no pool de saudação. Da mesma forma, se eDTUs extras não forem mais necessários, eles poderão ser removidos de um pool existente a qualquer momento. Você pode adicionar ou subtrair o pool de toohello de bancos de dados, ou o valor do limite de saudação do eDTUs de um banco de dados pode usar sob carga pesada tooreserve eDTUs para outros bancos de dados. Se um banco de dados é previsível subutilizados recursos, você pode movê-lo do pool de saudação e configurá-lo como um único banco de dados com uma quantidade previsível de recursos necessários.

## <a name="how-can-i-determine-hello-number-of-dtus-needed-by-my-workload"></a>Como determinar o número de saudação de DTUs necessários ao meu carga de trabalho?
Se você estiver procurando toomigrate local existente ou tooAzure de carga de trabalho de máquina virtual do SQL Server banco de dados SQL, você pode usar o hello [DTU Calculadora](http://dtucalculator.azurewebsites.net/) tooapproximate o número de saudação de DTUs necessário. Para uma carga de trabalho existente do banco de dados SQL, você pode usar [análise de desempenho de consulta de banco de dados SQL](sql-database-query-performance.md) toounderstand seu banco de dados recurso consumo (DTUs) tooget mais informações sobre como toooptimize sua carga de trabalho. Você também pode usar o hello [sys.dm_db_ resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) DMV tooget Olá consumo informações de recursos para Olá última hora. Olá como alternativa, o modo de exibição de catálogo [sys. resource_stats](http://msdn.microsoft.com/library/dn269979.aspx) podem também ser consultado tooget Olá mesmos dados para Olá últimos 14 dias, ainda que com uma menor fidelidade de médias de cinco minutos.

## <a name="how-do-i-know-if-i-could-benefit-from-an-elastic-pool-of-resources"></a>Como posso saber se eu teria benefícios com um pool elástico de recursos?
Pools também são indicados para um grande número de bancos de dados com padrões de utilização específicos. Para um determinado banco de dados, esse padrão é caracterizado por baixa utilização média com picos de utilização relativamente pouco frequentes. Banco de dados SQL avalia Olá históricos de uso dos bancos de dados em um servidor de banco de dados SQL e recomenda Olá configuração de pool apropriado no portal do Azure de saudação automaticamente. Para saber mais , confira [Quando um pool elástico deve ser usado?](sql-database-elastic-pool.md)

## <a name="what-happens-when-i-hit-my-maximum-dtus"></a>O que acontece quando eu atinjo o máximo de DTUs
Níveis de desempenho são calibrados e tooprovide controlados Olá necessária recursos toorun sua carga de trabalho do banco de dados para cima toohello limites máximo permitido para seu nível de camada e desempenho do serviço selecionado. Se sua carga de trabalho está atingindo os limites de saudação em um dos limites de dados de CPU/es/Log es, continuar recursos de saudação tooreceive nível Olá máximo permitido, mas são provavelmente toosee aumentado latências de suas consultas. Esses limites não resultam em erros, mas em vez disso, uma diminuição na carga de trabalho hello, a menos que lentidão Olá fica tão grave que consultas iniciam o tempo. Se você está atingindo os limites do máximo permitido de sessões/solicitações de usuários simultâneos (threads de trabalho), você verá erros explícitos. Confira [Limites de recursos do Banco de Dados SQL](sql-database-resource-limits.md) para saber mais sobre limite de recursos, além de CPU, memória, E/S de dados e E/S do log de transações.

## <a name="next-steps"></a>Próximas etapas
* Consulte [camada de serviço](sql-database-service-tiers.md) para obter informações sobre Olá DTUs e eDTUs disponível para bancos de dados único e pools elásticos.
* Confira [Limites de recursos do Banco de Dados SQL](sql-database-resource-limits.md) para saber mais sobre limite de recursos, além de CPU, memória, E/S de dados e E/S do log de transações.
* Consulte [análise de desempenho de consulta de banco de dados SQL](sql-database-query-performance.md) toounderstand seu consumo (DTUs).
* Consulte [visão geral do banco de dados SQL benchmark](sql-database-benchmark-overview.md) metodologia de saudação toounderstand por trás da carga de trabalho de parâmetro de comparação OLTP Olá usado Olá toodetermine DTU de mesclagem.
