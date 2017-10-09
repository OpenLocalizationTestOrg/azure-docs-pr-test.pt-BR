---
title: Limites de recursos de banco de dados SQL do aaaAzure | Microsoft Docs
description: "Esta página descreve alguns limites de recurso comuns para o Banco de Dados SQL do Azure."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 884e519f-23bb-4b73-a718-00658629646a
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2017
ms.author: carlrab
ms.openlocfilehash: 3e7be4fdc74e802d37274690531caaf138bcedb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-resource-limits"></a>Limites de recursos do Banco de Dados SQL do Azure
## <a name="overview"></a>Visão geral
Banco de dados SQL do Azure gerencia Olá recursos disponíveis tooa banco de dados usando dois mecanismos diferentes: **governança de recursos** e **imposição de limites**. Este tópico explica essas duas áreas principais do gerenciamento de recursos.

## <a name="resource-governance"></a>Governança de recursos
Uma das metas de design Olá das camadas de serviço Basic, Standard, Premium e RS Premium Olá é para o banco de dados do Azure SQL toobehave como se o banco de dados de saudação está em execução em sua própria máquina, isolada de outros bancos de dados. A governança de recursos emula esse comportamento. Se Olá agregados utilização de recursos atinge Olá máximo disponível da CPU, memória, e/s de Log e banco de dados de e/s de dados recursos toohello atribuído, administração do recurso de consultas de filas em execução e atribuir recursos toohello enfileirada consultas como eles liberar.

Como em um computador dedicado, utilizando os resultados de todos os recursos disponíveis em uma execução maior de consultas, em execução no momento, que pode resultar em tempos limite de comando no cliente de saudação. Aplicativos com lógica de repetição agressiva e aplicativos que executarem consultas no banco de dados de saudação com uma frequência alta podem encontrar mensagens de erros durante a tentativa de tooexecute novas consultas quando Olá limite de solicitações simultâneas foi atingido.

### <a name="recommendations"></a>Recomendações:
Monitorar utilização de recursos de saudação e tempos de resposta médio de saudação de consultas ao se aproximar Olá máxima utilização de um banco de dados. Quando encontrar latências maiores de consulta, você geralmente terá três opções:

1. Reduza o número de saudação de entrada solicitações toohello banco de dados tooprevent tempo limite e hello acumulação de solicitações.
2. Atribua um banco de dados de toohello nível mais alto desempenho.
3. Otimize a utilização de recursos de saudação consultas tooreduce de cada consulta. Para obter mais informações, consulte Olá seção ajuste/dicas de consulta no artigo de diretrizes de desempenho de banco de dados de SQL do Azure hello.

## <a name="enforcement-of-limits"></a>Imposição de limites
Os recursos, além da CPU, Memória, E/S de log e E/S de dados, são impostos pela negação de novas solicitações quando os limites são atingidos. Quando um banco de dados atinge o limite de tamanho máximo de saudação configurado, inserções e atualizações que aumentam o tamanho de dados falhar, enquanto seleciona e exclusões continuam toowork. Os clientes recebem um [mensagem de erro](sql-database-develop-error-messages.md) dependendo de limite de saudação foi atingido.

Por exemplo, número de saudação do banco de dados do SQL conexões tooa e número de saudação de solicitações simultâneas que podem ser processados são restritas. Banco de dados SQL permite o número de saudação de conexões toohello banco de dados toobe maior número de saudação do pool de conexão do toosupport de solicitações simultâneas. Enquanto o número de saudação de conexões que estão disponíveis facilmente possa ser controlado pelo aplicativo hello, Olá número de solicitações em paralelo geralmente é tooestimate mais difícil de vezes e toocontrol. Especialmente durante cargas de picos quando o aplicativo hello envia muitas solicitações ou banco de dados de saudação atinja os limites de recurso e começa a acumular threads de trabalho devido a consultas de execução toolonger, erros podem ser encontrados.

## <a name="service-tiers-and-performance-levels"></a>Camadas de serviço e níveis de desempenho
Há camadas de serviço e níveis de desempenho para o banco de dados individual e pools elásticos.

### <a name="single-databases"></a>Bancos de dados únicos
Para um único banco de dados, os limites de saudação do banco de dados são definidos por nível de desempenho e da camada de serviço de banco de dados do hello. Olá a tabela a seguir descreve as características de saudação de bancos de dados Basic, Standard, Premium e RS Premium em vários níveis de desempenho.

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

> [!IMPORTANT]
> Os clientes que usam níveis de desempenho P11 e P15 podem usar até too4 TB de armazenamento incluído sem custos adicionais. Essa opção de 4 TB está disponível no momento no hello seguintes regiões: US East2, oeste dos EUA, nos Gov Virgínia, Europa Ocidental, Alemanha Central, Sul Leste da Ásia, Leste do Japão, Leste da Austrália, Canadá Central e Leste do Canadá.
>

### <a name="elastic-pools"></a>Pools elásticos
[Pools Elásticos](sql-database-elastic-pool.md) compartilhar recursos entre bancos de dados no pool de saudação. Olá a tabela a seguir descreve as características de saudação de pools Elásticos Basic, Standard, Premium e RS Premium.

[!INCLUDE [SQL DB service tiers table for elastic databases](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Para uma definição expandida de cada recurso listada nas tabelas anteriores hello, consulte as descrições de saudação em [limites e recursos da camada de serviço](sql-database-performance-guidance.md#service-tier-capabilities-and-limits). Para obter uma visão geral das camadas de serviço, consulte [Camadas de serviço e níveis de desempenho do Banco de Dados SQL do Azure](sql-database-service-tiers.md).

## <a name="other-sql-database-limits"></a>Outros limites de Banco de Dados SQL
| Área | Limite | Descrição |
| --- | --- | --- |
| Bancos de dados usando a exportação Automatizada por assinatura |10 |Exportação automatizada permite que você toocreate uma agenda personalizada para fazer backup de bancos de dados SQL. visualização de saudação desse recurso terminará em 1 de março de 2017.  |
| Bancos de dados por servidor |Backup too5000 |Backup too5000 bancos de dados são permitidos por servidor. |
| DTUs por servidor |45000 |São permitidas 45.000 DTUs por servidor para o provisionamento de bancos de dados autônomos e pools elásticos. número total de saudação de bancos de dados independentes e pools permitidos por servidor é limitado somente pelo número de saudação do servidor DTUs.  

> [!IMPORTANT]
> A Exportação Automatizada do Banco de Dados SQL do Azure está agora em visualização e será desativada em 1º de março de 2017. Começando em 1º de dezembro de 2016, você não será capaz de tooconfigure automatizada de exportação em qualquer banco de dados SQL. Todos os trabalhos de exportação automatizada existente continuará toowork até 1º de março de 2017. Depois de 1º de dezembro de 2016, você pode usar [retenção de backup de longo prazo](sql-database-long-term-retention.md) ou [automação do Azure](../automation/automation-intro.md) bancos de dados do SQL tooarchive periodicamente usando o PowerShell periodicamente de acordo com o agendamento de tooa de sua escolha. Para um exemplo de script, você pode baixar Olá [exemplo de script do GitHub](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export).
>


## <a name="resources"></a>Recursos
[Assinatura do Azure e limites de serviços, cotas e restrições](../azure-subscription-service-limits.md)

[Faixas de Serviço de Banco de Dados SQL do Azure e Níveis de Desempenho](sql-database-service-tiers.md)

[Mensagens de erro para programas cliente do Banco de Dados SQL](sql-database-develop-error-messages.md)
